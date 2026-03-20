# Projects file

The `projects.json` file describes the repositories (grouped by project and data sources)
to be shown in the dashboards. It is composed of three levels:

  - First level: project names
  - Second level: data sources and metadata
  - Third level: data source URLs


This is an example of the content of a project's JSON file:

```json
{
    "Chaoss": {
        "gerrit": [
            "gerrit.chaoss.org --filter-raw=data.projects:CHAOSS"
        ]
        "git": [
            "https:/github.com/chaoss/grimoirelab-perceval",
            "https://<username>:<api-token>@github.com/chaoss/grimoirelab-sirmordred"
        ],
        "github": [
            "https:/github.com/chaoss/grimoirelab-perceval --filter-no-collection=true",
            "https:/github.com/chaoss/grimoirelab-sirmordred  --labels=[example]"
        ]
    },
    "GrimoireLab": {
        "gerrit": [
            "gerrit.chaoss.org --filter-raw=data.projects:GrimoireLab"
        ],
        "meta": {
            "title": "GrimoireLab",
            "type": "Dev",
            "program" : "Bitergia",
            "state": "Operating"
        },
    }
    "unknown": {
        "gerrit": [
            "gerrit.chaoss.org"
        ],
        "confluence": [
            "https://wiki.chaoss.org"
        ]
}
```

If you want to modify the file directly see the Projects section in the
[Mordred Configuration](../../mordred_configuration.md#projects-file) guide.

All the information needed to modify it can be found in the following [link from the
CHAOSS/GrimoireLab community](https://github.com/chaoss/grimoirelab-sirmordred#projectsjson-).
