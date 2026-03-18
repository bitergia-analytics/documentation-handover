# Supported Data Sources

Bitergia Analytics collects data from 30+ different platforms to give you a
holistic picture of the software development projects that matter to you. This
section would give you a brief idea of what data can be fetched and analyzed
from the different data sources.

  - [GitHub](github.md)
  - [GitLab](gitlab.md)
  - [Git](git.md)
  - [Stack Overflow](stackoverflow.md)
  - [Jira](jira.md)

You can also check out the data models of the supported data sources 
[upstream](https://github.com/chaoss/grimoirelab-elk/tree/master/schema).
Each CSV file has a minimum of two columns:

- `name` refers to the actual field. Eg `author_name`, `grimoire_creation_date`.
- `type` refers to the category of the field. Eg `boolean`, `long`.

Some CSV files have two additional columns:

- `aggregatable` refers to whether the field can be aggregated.
- `description` gives a brief about the field.
