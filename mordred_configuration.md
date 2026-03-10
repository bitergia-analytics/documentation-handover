# Mordred configuration

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

