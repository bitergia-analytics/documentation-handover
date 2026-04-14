# User Management

## Table of Contents

- [SortingHat](#sortinghat)
  - [Managing Users](#managing-users)
    - [Add user](#add-user)
    - [Add admin user](#add-admin-user)
    - [Remove User](#remove-user)
    - [Change permissions](#change-permissions)
    - [List users and roles](#list-users-and-roles)
    - [Change password](#change-password)
- [OpenSearch](#opensearch)
  - [Roles](#opensearch-roles)
  - [User management](#user-management)
    - [Add user](#add-user-1)
    - [Change password](#change-password)
    - [Delete user](#delete-user)

## SortingHat

All user management operations require first accessing the SortingHat container:

```bash
docker exec -ti bap_sortinghat /bin/bash
```

### About Multitenant Mode

SortingHat can operate in two modes:

- **Single-tenant mode (default)**: All users and data belong to a single
organization. Most users will use this mode.
- **Multitenant mode**: Multiple organizations (tenants) can be managed
within the same SortingHat instance, with data isolation between them.
This is typically used in enterprise or SaaS deployments.

To determine whether your SortingHat instance is running in multitenant
mode, check the `vars.yml` file in your Ansible configuration. You may
find the variable `sortinghat_multi_tenant` set to `true` and, under
`instances.sortinghat.tenant`, the name of the tenant.


### Add user

Add a new user to SortingHat.

#### For single-tenant mode
```bash
/opt/venv/bin/sortinghat-admin create-user
```

#### For multitenant mode

```bash
/opt/venv/bin/sortinghat-admin create-user
/opt/venv/bin/sortinghat-admin set-user-tenant <user> <tenant> <tenant>
```

### Add admin user

Add a new admin user to SortingHat.

#### For single-tenant mode
```bash
/opt/venv/bin/sortinghat-admin create-user --is-admin
```

#### For multitenant mode
```bash
/opt/venv/bin/sortinghat-admin create-user --is-admin
/opt/venv/bin/sortinghat-admin set-user-tenant <user> <tenant> <tenant>
```

### Remove User

Remove a user from SortingHat.

```bash
export DJANGO_SETTINGS_MODULE=sortinghat.config.settings
/opt/venv/bin/django-admin shell
```

```python
from django.contrib.auth.models import User
user = User.objects.get(username="<user>")
user.delete()
```

### Change permissions

Assign a role to a user. Available roles:

- `admin`: Full access (view, add, change, delete).
- `user`: Full access except executing jobs and periodic tasks.
- `readonly`: View-only access.

#### For single-tenant mode
```bash
/opt/venv/bin/sortinghat-admin set-user-permissions <user> <role>
```

#### For multitenant mode
```bash
/opt/venv/bin/sortinghat-admin set-user-permissions <user> <role> --tenant <tenant>
```

### List users and roles

List all SortingHat users and their assigned roles.

```bash
export DJANGO_SETTINGS_MODULE=sortinghat.config.settings
/opt/venv/bin/django-admin shell
```

#### For single-tenant mode

Copy and paste the following code snippet to list all users and their roles:

```python
from django.contrib.auth import get_user_model

for user in get_user_model().objects.prefetch_related('groups').all():
    if user.is_superuser:
        group_id = 'admin'
    else:
        group_id = user.groups.values_list('name', flat=True).first() or 'no_group'
    
    print(f"{user.username}: {group_id}")
```

#### For multitenant mode

Copy and paste the following code snippet to list all users, their roles:

```python
from django.contrib.auth import get_user_model

for user in get_user_model().objects.all():
    if user.is_superuser:
        permission_group = 'admin'
    else:
        try:
            tenant_record = Tenant.objects.filter(user=user).first()
            permission_group = tenant_record.perm_group if tenant_record else None
        except Tenant.DoesNotExist:
            permission_group = None
    print(f"{user.username}: {permission_group}")
```

### Change password

Users can change their own password through the SortingHat UI. However, if an administrator
needs to reset a user's password, they can do so through the Django shell.

This process is the same for both single-tenant and multitenant deployments.

```bash
export DJANGO_SETTINGS_MODULE=sortinghat.config.settings
/opt/venv/bin/django-admin shell
```

```python
from django.contrib.auth.models import User
user = User.objects.get(username="<user>")
user.set_password("<new_password>")
user.save()
```

# OpenSearch

## OpenSearch Roles

OpenSearch uses two key concepts for access control:

- **Roles**: Define permissions and access levels to indices, documents, and 
operations within OpenSearch. Roles specify what actions a user can perform 
(read, write, delete, etc.) and on which resources.

- **Backend roles**: Labels assigned to users that map them to OpenSearch
roles. When a user is assigned a backend role (e.g., `<tenant>_user`),
OpenSearch automatically grants them the permissions associated with the
corresponding role (e.g., `bap_<tenant>_user_role`).

In the context of BAP (Bitergia Analytics Platform), backend roles act as
the bridge between user accounts and their functional permissions through
predefined roles.

The following roles are available for OpenSearch:

- **`bap_<tenant>_user_role`**: Read-only access to tenant data. Users with
this role can view dashboards and visualizations.
  - Backed role assigned: `<tenant>_user`

- **`bap_<tenant>_privileged_user_role`**: Read and write access to tenant
data. Users with this role can view and modify dashboards and visualizations.
  - Backed role assigned: `<tenant>_privileged_user`

- **`bap_<tenant>_pseudonymize_role`**: Access to pseudonymized data. This
role allows users to work with data where personal information has been masked.
  - Backed role assigned: `<tenant>_pseudonymize`

- **`bap_<tenant>_mordred_role`**: Service account role used by the Mordred
component for data ingestion and processing. This role has the necessary
permissions to write and update indices.

- **`bap_<tenant>_anonymous_access_role`**: Limited read-only access for
unauthenticated users. This role is used when anonymous access is enabled.
  - Backed role assigned: `opendistro_security_anonymous_backendrole`

Replace `<tenant>` with your actual tenant name when assigning these roles.


## User management

All user management operations are performed through the OpenSearch Dashboards UI.

For more information about user and role management, refer to the [OpenSearch documentation](https://docs.opensearch.org/latest/security/access-control/users-roles/).

### Add user

To add a new user to OpenSearch Dashboards:

1. Access the OpenSearch Dashboards UI at your instance URL
2. Navigate to **Security** > **Internal users**
3. Click **Create internal user**
4. Fill in the user details:
    - Username
    - Password
    - Backend roles
        - `admin`: admin (role: `all_access`)
        - `<tenant>_user`: Read user (role: `bap_<tenant>_user_role`)
        - `<tenant>_privileged`: Read/write user (role: `bap_<tenant>_privileged_user_role`)
5. Click **Create**

### Change password

To change a user's password:

1. Navigate to **Security** > **Internal users**
2. Click on the username
3. Click **Edit**
4. Enter the new password
5. Click **Submit**

### Delete user

To remove a user:

1. Navigate to **Security** > **Internal users**
2. Select the user(s) to delete
3. Click **Delete**
4. Confirm the deletion
