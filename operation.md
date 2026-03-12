# Operation

This guide explains how to create infrastructure using the BAP
([Bitergia Analytics Platform Toolkit](https://github.com/bitergia-analytics/bap-deployment-toolkit)) and some of the basic actions to operate the platform.

All paths are referenced from the clone of `bap-deployment-toolkit` directory.

> **Note**: This guide provides a quick reference for common operations.

## Table of Contents

- [Control Node](#control-node)
- [Upgrading BAP Versions](#upgrading-bap-versions)
- [Mordred Operations](#mordred-operations)
  - [Restarting Mordred Container (Automated)](#restarting-mordred-container-automated)
  - [Restarting Mordred Container (Manual)](#restarting-mordred-container-manual)
  - [Updating Mordred Configuration](#updating-mordred-configuration)

## Control Node

The **Control Node** is the machine from which you manage and orchestrate the
BAP infrastructure. It contains the OpenTofu configurations for provisioning
cloud resources and Ansible playbooks for deploying and configuring services
on those resources. All infrastructure management commands are executed from
this node. Here are the key components for managing the Control Node:

- [OpenTofu](https://github.com/bitergia-analytics/bap-deployment-toolkit/blob/main/docs/provision.md):
Infrastructure provisioning.
- [Ansible](https://github.com/bitergia-analytics/bap-deployment-toolkit/blob/main/docs/deployment_and_config.md):
Deployment and configuration management.

## Upgrading BAP Versions

On the `control-node`, you can upgrade BAP versions by following these steps.
All commands must be executed from the `ansible` directory:

1. Stop the Mordred container

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
   ```

1. Update the BAP versions at `environments/<project>/inventory/vars.yml`

   ```yaml
    # BAP versions
    bap_version: 0.38.1
    opensearch_version: 0.38.1
    opensearch_dashboards_version: 0.38.1
    sortinghat_version: 0.38.1
    sortinghat_worker_version: 0.38.1
   ```

1. Comment out the services that you don't want to upgrade from `all_in_one.yml`.
   Normally, `mariadb`, `redis` (it uses `valkey`, but the name is still redis),
   and `monitoring` do not upgrade their versions.
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

1. If you are not using `all-in-one` infrastructure, then you need to comment
   out the services from `all.yml`.

   ```yaml
   #- import_playbook: mariadb.yml
   #- import_playbook: redis.yml
   - import_playbook: opensearch.yml
   - import_playbook: opensearch_dashboards.yml
   - import_playbook: sortinghat.yml
   - import_playbook: sortinghat_worker.yml
   - import_playbook: nginx.yml
   - import_playbook: mordred.yml
   #- import_playbook: monitoring.yml
   ```

1. Run the playbooks to apply the new versions:

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/all_in_one.yml
   ```

   or

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/all.yml
   ```

## Mordred Operations

### Restarting Mordred Container (Automated)

This is the recommended method for restarting the Mordred container:

1. Stop the Mordred container

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
   ```

1. Start the mordred container

   If you are using `all-in-one` infrastructure, you need to run the
   `playbooks/all_in_one.yml` playbook, but first comment out the rest of the
   services except mordred.

   ```yaml
   - hosts: all_in_one
     roles:
       #- mariadb
       #- redis
       #- opensearch
       #- opensearch_dashboards
       #- sortinghat
       #- sortinghat_worker
       #- nginx
       - mordred
       #- monitoring
     become: true
   ```

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/all_in_one.yml
   ```

   If you are using separate infrastructure, you need to run the
   `playbooks/mordred.yml` playbook.

   ```bash
   ansible-playbook -i environments/<project>/inventory playbook/mordred.yml
   ```

### Restarting Mordred Container (Manual)

1. On the `control-node`
   1. stop the mordred container

      ```bash
      ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
      ```

1. On the `all-in-one-0` or `mordred-0` node (depending on your infrastructure):
   1. Switch to sudo `sudo su`
   1. Fetch updated `setup.cfg`

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
      docker start <container_name>
      ```

### Updating Mordred Configuration

When you update the `setup.cfg` file, you need to [restart the Mordred container](#restarting-mordred-container-automated).
If the `mordred-0` or `all-in-one-0` machine lacks permission to pull
changes from the `setup.cfg` repository, follow the [manual restart procedure](#restarting-mordred-container-manual).

> **IMPORTANT**: 
> - When you update the `setup.cfg` file, you **must** restart the Mordred container.
> - When you update the `projects.json` file, Mordred will automatically detect the changes and update the index, so no container restart is required.
