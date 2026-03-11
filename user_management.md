# User Management

## Table of Contents

- [SortingHat](#sortinghat)
  - [Managing Users](#managing-users)
    - [Add user](#add-user)
    - [Add admin user](#add-admin-user)
    - [Remove User](#remove-user)
    - [Change permissions](#change-permissions)
- [OpenSearch](#opensearch)
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

# OpenSearch

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
