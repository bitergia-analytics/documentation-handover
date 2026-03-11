# Operation

This guide explains how to create infrastructure using the BAP ([Bitergia Analytics Platform](https://github.com/bitergia-analytics/bap-deployment-toolkit)).

All paths are referenced from the clone of `bap-deployment-toolkit` directory.


## Table of Contents

- [Control Node](#control-node)
   - [OpenTofu](#opentofu)
   - [Ansible](#ansible)
- [Mordred](#mordred)

# Control Node

The **Control Node** is the machine from which you manage and orchestrate the
BAP infrastructure. It contains the OpenTofu configurations for provisioning
cloud resources and Ansible playbooks for deploying and configuring services
on those resources. All infrastructure management commands are executed from
this node.

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

Depending on your infrastructure type, the Mordred container runs either on the
`all-in-one-0` node or on a separate `mordred-0` node. However, the steps to check for issues
and/or restart the Mordred container are the same.

How to apply changes when you update the Mordred `setup.cfg` file:

1. On the `control-node`
   1. stop the mordred container

      ```bash
      ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
      ```

1. On the `all-in-one-0` or `mordred-0` node (depending on your infrastructurere):
   1. Switch to sudo `sudo su`
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

**IMPORTANT**: When you update the `setup.cfg` file, you must restart the
mordred container, but if you update the `projects.json` file, mordred will
automatically pull the changes and update the index, so you don't need to
restart the mordred container.
