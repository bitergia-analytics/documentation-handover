# Mordred configuration

[Mordred](https://github.com/chaoss/grimoirelab-sirmordred) is the orchestrator component of GrimoireLab that coordinates the entire
data pipeline for software development analytics. It manages the collection of raw
data from various sources (Git repositories, GitHub issues, pull requests, etc.),
enriches this data with additional metrics, and uses SortingHat to unify contributor
information across different data sources.

GrimoireLab supports many datasources, but this guide will focus on examples for Git and GitHub. For complete documentation on all supported datasources and configuration options, refer to the [SirMordred documentation](https://github.com/chaoss/grimoirelab-sirmordred?tab=readme-ov-file#sirmordred---) and 
[Bitergia backends](https://github.com/bitergia-analytics/bitergia-analytics-elk-backends/blob/main/README.md).

- [Configuration File](#configuration-file)
- [Projects file](#projects-file)
- [Data source examples](#data-source-examples)
  - [Git](#git)
  - [GitHub](#github)

## Configuration File

Mordred uses a configuration file (`setup.cfg`) to define the datasources to analyze and their parameters.
It is available under `/docker/mordred/setups/`.

The configuration file is organized into multiple sections:
- **[general]**: Basic setup (debug mode, logs)
- **[projects]**: Where your projects.json file is located
- **[es_collection]** & **[es_enrichment]**: OpenSearch connection details
- **[sortinghat]**: Identity configuration
- **[phases]**: Enable/disable pipeline stages (collection, enrichment, identities)
- **Backend sections**: One per datasource (e.g., [git], [github]) with indices and parameters. Each datasource could contain several studies that must be defined.

See the [related section in the GrimoireLab tutorial](https://chaoss.github.io/grimoirelab-tutorial/docs/getting-started/setup-cfg).

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

See:
 - The [related section in the GrimoireLab tutorial](https://chaoss.github.io/grimoirelab-tutorial/docs/getting-started/projects-json/).
 - Some [topics related to the management of this file](https://github.com/bitergia-analytics/documentation-handover/blob/main/end-user-doc/new/faq.md#data-sources-management).

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

The `github2:issue` backend is used to collect comments from GitHub issues and pull requests. It shares the same raw index as `github:issue` but uses a separate enriched index to store comment-specific information. If they share the same raw index, `collect` must be set to false to prevent duplicate data collection. The same applies to `github2:pull`.

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


## Utilities related to the mainteinance of the project file

Bitergia has been collecting [utility scripts](https://gitlab.com/Bitergia/devops/sources-utils)
for a number of internal usage needs related to the mainteinance of the project file.

 
## Applying retroactive modifications

Usually Mordred runs a neverending loop, so changes in the projects file apply
to the data loaded from the next loop on.

If you want to apply them retroactively to the previously loaded data,
you typically use an `update_by_query`.

OpenSearch Dashboards provides an applet on its web interface called **Dev Tools**.
It is in the group "Management" of the dropdown menu on the top-left corner of the window.

For example, changes in project names can be updated using this query:
```json
POST <INDEX ALIAS>/_update_by_query?wait_for_completion=false
{
  "query": {
    "match": {
      "project": "<OLD project name>"
    }
  },
  "script": {
    "source": "ctx._source.project = params.new; ctx._source.project_1 = params.new",
    "lang": "painless",
    "params": {
      "new": "<NEW project name>"
    }
  }
}
```

Tips:

When available, the `_all_enriched` alias will cover most, if not all of the indexes
except the results of studies, such as `_all_onion` or `_git_areas_of_code`.

Send `GET _tasks/<ID>` to watch the task run (status).

Typically, you do this while Mordred is running in the background.
Note that the running Mordred is still working according to the old configuration,
so it might still smear the data. The most pragmatic solution is to wait for the
current cycle to end and then run query.
