# SortingHat

## Managing Users

All user management operations require first accessing the SortingHat container:

```bash
docker exec -ti bap_sortinghat /bin/bash
```

### Add user

Add a new user to SortingHat. If multitenant mode is enabled, users must be assigned to the related tenant.

```bash
/opt/venv/bin/sortinghat-admin create-user
/opt/venv/bin/sortinghat-admin set-user-tenant <user> <tenant> <tenant>
```

### Add admin user

Add a new admin user to SortingHat. If multitenant mode is enabled, users must be assigned to the related tenant.

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

Assign a role to a user in a specific tenant. Roles can be `user`, `admin`, or `readonly`.

- `admin`: Full access (view, add, change, delete).
- `user`: Full access except executing jobs and periodic tasks.
- `readonly`: View-only access.

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

## Index management

### Custom indices

Indices following these naming patterns are tenant-specific custom indices:
- `custom_<tenant>_*`
- `c_<tenant>_*`

**Visibility**: These indices are accessible to users with the following backend roles:
- `<tenant>_user`: Read access
- `<tenant>_privileged`: Read/write access

Otherwise, they will only be visible to admin users.


# Mordred configuration

GrimoireLab supports many datasources, but this guide will focus on examples for Git and GitHub. For complete documentation on all supported datasources and configuration options, refer to the [SirMordred documentation](https://github.com/chaoss/grimoirelab-sirmordred?tab=readme-ov-file#sirmordred---) and 
[Bitergia backends](https://github.com/bitergia-analytics/bitergia-analytics-elk-backends/blob/main/README.md).

## Configuration File

Mordred uses a configuration file (`setup.cfg`) to define the datasources to analyze and their parameters.
It is available under `/docker/mordred/setups/`.

The configuration file is organized into multiple sections: general configuration sections (`general`, `projects`, `es_collection`, `es_enrichment`, `sortinghat`, and `phases`), and datasource specific sections (backends and studies).

The configuration file is organized into multiple sections:
- **[general]**: Basic setup (debug mode, logs)
- **[projects]**: Where your projects.json file is located
- **[es_collection]** & **[es_enrichment]**: OpenSearch connection details
- **[sortinghat]**: Identity configuration
- **[phases]**: Enable/disable pipeline stages (collection, enrichment, identities)
- **Backend sections**: One per datasource (e.g., [git], [github]) with indices and parameters. Each datasource could contain several studies that must be defined.

## Projects file

The projects file (`projects.json`) defines which repositories and datasources should be analyzed by Mordred.
It is available under `/docker/mordred/instances/<project_name>/sources`.

The file uses a JSON structure to organize projects and their datasources. Each project can include multiple repositories from different platforms.

Each datasource key in `projects.json` must have a corresponding section in `setup.cfg`. 

For example, if your `projects.json` includes:
```json
{
  "Project": {
    "git": [...],
    "github:issue": [...]
  }
}
```

Then your `setup.cfg` must contain matching sections:
```ini
[git]
# git configuration

[github:issue]
# github issue configuration
```

## Data source examples

Below are some examples for Git and GitHub data sources. For the complete list of supported datasources and their configuration options, see the [official list of supported data sources](https://github.com/chaoss/grimoirelab-sirmordred?tab=readme-ov-file#supported-data-sources-).

### Git

Analyze Git repositories to extract commit data, authors, and code evolution.

*Note*: If you want to analyze private git repositories, make sure you pass the credentials directly in the URL.

- `setup.cfg`

  ```ini
  [git]
  raw_index = git_raw
  enriched_index = git_enriched
  latest-items = true
  studies = [enrich_demography:git]

  [enrich_demography:git]
  ```

- `projects.json`
  ```json
  {
    "Project Name 1": {
      "git": [
        "https://github.com/chaoss/grimoirelab"
      ]
    },
    "Project Name 2": {
      "git": [
        "https://github.com/chaoss/grimoirelab-perceval"
      ]
    }
  }
  ```

### GitHub

Collect data from GitHub including issues, pull requests and repos.

GitHub's REST API considers every pull request an issue, but not every issue is a pull request. For this reason, **issue** category may contain both issues and pull requests.

The `github2:issue` backend is used to collect comment GitHub issues and pull requests. It shares the same raw index as `github:issue` but uses a separate enriched index to store comment-specific information. If they share the same raw index, `collect` must be set to false to prevent duplicate data collection the same for `github2:pull`.

The `github:repo` backend collects repository-level metadata from GitHub. It collects only the latest repository statistics (stars, forks, watchers, etc.). To track repository evolution over time, this backend must be run periodically.

- `setup.cfg`
  ```ini
  [github:issue]
  raw_index = github-issue_raw
  enriched_index = github-issue_enriched
  category = issue
  api-token = [xxxx, yyyy]
  sleep-for-rate = true

  [github2:issue]
  collect = false
  raw_index = github-issue_raw
  enriched_index = github2-issue_enriched
  category = issue
  api-token = NOT-NEEDED
  sleep-for-rate = true

  [github:pull]
  raw_index = github-pull_raw
  enriched_index = github-pull_enriched
  category = pull_request
  api-token = [xxxx, yyyy]
  sleep-for-rate = true

  [github2:pull]
  collect = false
  raw_index = github-pull_raw
  enriched_index = github2-pull_enriched
  category = pull_request
  api-token = NOT-NEEDED
  sleep-for-rate = true

  [github:repo]
  raw_index = github-repo_raw
  enriched_index = github-repo_enriched
  category = repository
  api-token = [xxxx, yyyy]
  sleep-for-rate = true
  ```

- `projects.json`
  ```json
  {
    "Project Name": {
      "github:issue": [
        "https://github.com/chaoss/grimoirelab"
      ],
      "github:pull": [
        "https://github.com/chaoss/grimoirelab"
      ],
      "github2:issue": [
        "https://github.com/chaoss/grimoirelab"
      ],
      "github2:pull": [
        "https://github.com/chaoss/grimoirelab"
      ],
      "github:repo": [
        "https://github.com/chaoss/grimoirelab"
      ]

    }
  }
  ```

# Mordred common issues

## Pontoon session id expired

Pontoon does not provide API tokens or personal access tokens. Authentication must be performed using the Django session cookie (`sessionid`) generated after logging into the web interface.

The `sessionid` cookie remains valid for 14 days. After expiration, the login process must be repeated and a new session ID retrieved.

### Obtaining the Session ID

- Log in (or create an account) at https://pontoon.mozilla.org/
- Open your browser’s Developer Tools (F12).
- Retrieve the `sessionid` cookie:
  - Application/Storage > Cookies > pontoon.mozilla.org > sessionid

### Using the Session ID

- Open the `setup.cfg` file
- Update the field `session-id` under `[pontoon]` section:
  ```
  [pontoon]
  ...
  session-id = <your-session-id>
  ```

## Bugzillarest error

During data collection from BugzillaREST, the API may occasionally return internal errors that interrupt the collection process.

These failures are temporary but may persist for hours, days, or even weeks before the endpoint becomes usable again.

### Error in logs

The failure usually appears in the logs as:

```
2025-09-08 09:28:21,511 - Project - grimoire_elk.elk - ERROR - Error feeding raw from bugzillarest (https://bugzilla.mozilla.org): 400 Client Error: Bad Request for url: https://bugzilla.mozilla.org/rest/bug?last_change_time=2025-09-02T17%3A53%3A02Z&limit=1&order=changeddate&include_fields=_all&offset=1
```

This typically indicates that one or more items returned by the API cannot be processed correctly.

### Workaround

The workaround is to skip the problematic item(s) and resume the collection from a later timestamp.

1. Identify the timestamp where the failure occurs from the logs.

2. Test the endpoint using Perceval, starting from that timestamp and retrieving a single bug:

```
perceval bugzillarest https://bugzilla.mozilla.org \
  --max-bugs 1 \
  --from-date 2025-09-24T06:47:16+00:00 \
  --no-archive \
  -t <token>
```

3. Increment the `last_change_time` value until the request succeeds. Try to adjust the timestamp at the minute level to identify the first valid item and minimize the number of skipped items.

4. Update the `from-date` parameter in `setup.cfg` to the working timestamp:
   ```
   [bugzillarest]
   ...
   from-date = YYYY-MM-DDTHH:MM:SS+00:00
   ```
5. Restart the collection process.
