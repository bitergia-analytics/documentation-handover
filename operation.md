# Control Node

This guide explains how to create infrastructure using the BAP ([Bitergia Analytics Platform](https://github.com/bitergia-analytics/bap-deployment-toolkit)).

All paths are referenced from the `bap-deployment-toolkit` directory.

## OpenTofu

Machines, buckets, and networks are created by OpenTofu at `opentofu/environments/<project>/`.
The important file here is `environments.tf`, where you will have a similar file as:

```yaml
module "bap_env_aws" {
  source = "../../modules/bap_env_aws"

  prefix = "test"

  # GCP Only
  zone             = var.zone
  persistent_disks = true

  # AWS Only
  region                = var.region
  availability_zone     = "eu-north-1a"
  ami_id                = "ami-0a3ad108ca9a42423"
  key_name              = "bap-ssh"
  delete_on_termination = false

  all_in_one_node_count    = 1
  # GCP
  all_in_one_machine_type = "e2-standard-4"
  # AWS
  all_in_one_instance_type = "m5.xlarge"

  # Set to 0 the rest of the services
  mariadb_node_count = 0
  redis_node_count = 0
  opensearch_manager_node_count = 0
  opensearch_data_node_count = 0
  opensearch_dashboards_node_count = 0
  opensearch_dashboards_anonymous_node_count = 0
  nginx_node_count = 0
  mordred_node_count = 0
  sortinghat_node_count = 0
  sortinghat_worker_node_count = 0
}

output "bap_env_aws" {
  value = module.bap_env_aws
}
```

If you want to change the infrastructure, you can modify this file and run OpenTofu commands to apply it.

```bash
tofu apply
```

According to the file, it will create one machine named `all_in_one` plus two
buckets (SortingHat and backups) and network configurations.

You can find more info at https://github.com/bitergia-analytics/bap-deployment-toolkit/blob/main/docs/provision.md

## Ansible

When the infrastructure is created, Ansible will deploy and configure the machines.

There are two files at `ansible/environments/<project>/inventory`:

- `<project>.gcp.yml` | `<project>.aws_ec2.yml`: Dynamic inventory (GCP | AWS)
- `vars.yml`: All BAP configurations

This is the `vars.yml` file (the same for GCP or AWS), but only some parameters are shown:

```yaml
all:
  vars:
    # Ansible Settings
    # **GCP** - SSH username for the Service Account, in the format `sa_<ID>`
    # **AWS** - `admin`.
    ansible_user: "<service_account_ssh_user>"
    ansible_ssh_private_key_file: "<path_to_ssh_key>"

    # GCP only
    project_id: "<project_name>"

    # AWS only
    aws_region: "<aws_region>"

    # BAP versions
    bap_version: 0.38.1
    opensearch_version: 0.38.1
    opensearch_dashboards_version: 0.38.1
    sortinghat_version: 0.38.1
    sortinghat_worker_version: 0.38.1

    # Passwords and credentials
    mariadb_root_password: <mariadb_root_password>
    redis_password: <redis_password>
    opensearch_admin_user: <admin_username>
    opensearch_admin_password: <admin_password>
    sortinghat_superuser_name: <sortinghat_admin_username>
    sortinghat_superuser_password: <sortinghat_admin_password>

    # OpenSearch Heap
    opensearch_cluster_manager_heap_size: <opensearch_cluster_manager_heap_size>

    ## Buckets
    backups_assets_bucket: <backups_assets_bucket>
    sortinghat_assets_bucket: <sortinghat_assets_bucket>

    # Mordred Settings
    mordred_setups_repo_url: <repo_mordred_config.git>

    # Instances Settings
    instances:
    - project: <project>
      tenant: <tenant>
      public: false
      mordred:
        password: <mordred_tenant_a_password>
        sources_repository: "<repo_projects.git>"
        host: 0
      sortinghat:
        tenant: <tenant>
      nginx:
        fqdn: <fqdn>
        http_rest_api: false
```

You can find more info at https://github.com/bitergia-analytics/bap-deployment-toolkit/blob/main/docs/deployment_and_config.md

Steps to upgrade BAP versions (all commands must be executed under the `ansible` directory):

1. Stop mordred container

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
   ```

1. Update the BAP versions at `vars.yml`

   ```yaml
    # BAP versions
    bap_version: 0.38.1
    opensearch_version: 0.38.1
    opensearch_dashboards_version: 0.38.1
    sortinghat_version: 0.38.1
    sortinghat_worker_version: 0.38.1
   ```

1. Comment out the services that you don't want to upgrade from `all_in_one.yml`.
   Normally, `mariadb`, `redis`, and `monitoring` do not upgrade their versions.
   **IMPORTANT**: When you upgrade `sortinghat`, you must run `nginx` too.

   ```yaml
   - hosts: all_in_one
     roles:
       #- mariadb
       #- redis
       - opensearch
       - opensearch_dashboards
       - sortinghat
       - sortinghat_worker
       - nginx
       - mordred
       #- monitoring
     become: true
   ```

1. Run the playbooks to apply the new versions:

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/all_in_one.yml
   ```

# Mordred

Depends on which kind of infrastructure you have the mordred container in the `all-in-one` or in a separated node `mordred-0`, but the steps to check the issues and/or restart the mordred container are the same.

How to apply when you update the Mordred `setup.cfg` file.

1. On the `control-node`
   1. stop the mordred container

      ```bash
      ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
      ```

1. On the `all-in-one` or `mordred-0` node depends on your infrastructure:
   1. Change to sudo `sudo su`
   1. Update `setup.cfg`

      ```bash
      cd /docker/mordred/setups
      git pull origin main
      ```

   1. Get the mordred container

      ```bash
      docker ps -a | grep mordred
      ```

   1. Start the mordred container

      ```bash
      docker start <container_name | container_ID>
      ```

## Common Issues

**IMPORTANT**: When you update the `setup.cfg` file, you must restart the
mordred container, but if you update the `projects.json` file, mordred will
automatically pull the changes and update the index, so you don't need to
restart the mordred container.

### The index is not updated

If the index is not updated, you can check the logs to find out the issue at
`/docker/mordred/instances/test/logs/all.log`.

- For example, if you want to see the logs of the `git` thread, you can filter
 the logs with `grep`:

```bash
root@all-in-one-0:~# cd /docker/mordred/instances/test/logs
root@all-in-one-0:/docker/mordred/instances/test/logs# cat all.log | grep -v autorefresh | grep git] | tail
```

Maybe you don't have permissions to clone the repository or it does not exist.

### Unhealthy mordred container

If the mordred container is unhealthy, you can check the logs to find out the
issue at `/docker/mordred/instances/test/logs/all.log`.

```bash
root@all-in-one-0:~# docker ps

CONTAINER ID   IMAGE                                COMMAND                  CREATED       STATUS                    PORTS     NAMES
969a90b912a1   bitergia/bitergia-analytics:0.37.0   "/bin/sh -c ${DEPLOY…"   3 weeks ago   Up 22 hours (unhealthy)             mordred_test
```

When the mordred container is unhealthy, is because the Task Manager is not
able to connect to OpenSearch, and the thread will be stop, in this case the
`github2:issue` and `git` threads.

```bash
root@bitergio-mordred-1:/docker/mordred/instances/sta/logs# cat all.log | grep ERROR | grep "Task Manager"

2026-03-09 15:30:30,394 - Test - sirmordred.task_manager - ERROR - [github2:issue] Exception in Task Manager 500 Server Error: Internal Server Error for url: https://bap-opensearch-manager-0:9200/bap_test_github2-issue_260122_enriched_260122/_update_by_query?wait_for_completion=true&conflicts=proceed

2026-03-09 15:30:37,333 - Test - sirmordred.task_manager - ERROR - [git] Exception in Task Manager TransportError(500, 'search_phase_execution_exception', 'node [cv1rlvDRSd6SwWdm8vPJrx] is not available')
```

To solve this issue, you can restart the mordred container.

1. On the `control-node`
   1. stop the mordred container

      ```bash
      ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
      ```

1. On the `all-in-one` or `mordred-0` node depends on your infrastructure:
   1. Change to sudo `sudo su`
   1. Start the mordred container

      ```bash
      docker start mordred_test
      ```
