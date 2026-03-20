# GitHub Issues Data Model

This index contains one document per GitHub issue.

All the field types are aggregatable except the `text` field type. Those are:

  - `title_analyzed`.
  - `issue_title_analyzed`.
  - `body_analyzed`.

| **Name**                    | **Type**  | **Description**                                                                                               |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------|
| _Cross-references fields_   | NA        | Fields coming from cross-references study (available only when it is active), see [cross_references.csv](https://github.com/chaoss/grimoirelab-elk/blob/master/schema/cross_references.csv).       |
| assignee_data_bot           | boolean   | True/False if the assignee is a bot or not.                                                                   |
| assignee_data_domain        | keyword   | Assignee's domain name from SortingHat profile.                                                               |
| assignee_data_id            | keyword   | Assignee's id from SortingHat profile.                                                                        |
| assignee_data_name          | keyword   | Assignee's name.                                                                                              |
| assignee_data_org_name      | keyword   | Assignee's organization name from SortingHat profile.                                                         |
| assignee_multi_org_names    | keyword   | List of the assignee organizations from the SortingHat profile.                                               |
| assignee_data_user_name     | keyword   | Assignee's username from SortingHat profile.                                                                  |
| assignee_data_uuid          | keyword   | Assignee's UUID from SortingHat profile.                                                                      |
| assignee_domain             | keyword   | Assignee's domain name from GitHub.                                                                           |
| assignee_geolocation        | geo_point | Assignee's global location using coordinates.                                                                 |
| assignee_location           | keyword   | Assignee's geographical location.                                                                             |
| assignee_login              | keyword   | Assignee's login name from GitHub.                                                                            |
| assignee_name               | keyword   | Assignee's name from GitHub.                                                                                  |
| assignee_org                | keyword   | Assignee's organization name from GitHub.                                                                     |
| author_bot                  | boolean   | True/False if the author is a bot or not.                                                                     |
| author_domain               | keyword   | Author's domain name from SortingHat profile.                                                                 |
| author_id                   | keyword   | Author's ID from SortingHat profile.                                                                          |
| author_name                 | keyword   | Author's name.                                                                                                |
| author_org_name             | keyword   | Author's organization name from SortingHat profile.                                                           |
| author_multi_org_names      | keyword   | List of the author organizations from SortingHat profile.                                                     |
| author_user_name            | keyword   | Author's username from SortingHat profile.                                                                    |
| author_uuid                 | keyword   | Author's UUID from SortingHat profile.                                                                        |
| closed_at                   | date      | Date when an issue was closed.                                                                                |
| created_at                  | date      | Date when an issue was opened.                                                                                |
| demography_max_date         | date      | Date of the latest issue of the corresponding author. Available only when demography study is active.         |
| demography_min_date         | date      | Date of the first (oldest) issue of the corresponding author. Available only when demography study is active. |
| github_repo                 | keyword   | The name of the GitHub repository.                                                                            |
| grimoire_creation_date      | date      | Issue creation date.                                                                                          |
| id_in_repo                  | keyword   | The issue's ID in the repository it was created.                                                              |
| id                          | long      | Issue's ID in GitHub.                                                                                         |
| is_github_issue             | long      | Used to separate issues from other items such as pull requests.                                               |
| issue_url                   | keyword   | Full URL of the issue.                                                                                        |
| item_type                   | keyword   | The type of the item (`issue`/`pull_request`).                                                                    |
| labels                      | keyword   | The labels assigned to an issue.                                                                              |
| metadata__enriched_on       | date      | Date when the data were enriched.                                                                             |
| metadata__gelk_backend_name | keyword   | Name of the backend used to enrich the data.                                                                  |
| metadata__gelk_version      | keyword   | Version of the backend used to enrich the data.                                                               |
| metadata__timestamp         | date      | Date when the item was stored in ElasticSearch raw index.                                                     |
| metadata__updated_on        | date      | Date when the item was updated on its original data source.                                                   |
| origin                      | keyword   | The original URL from which the repository was retrieved.                                                     |
| painless_delay              | float     | Real-time open days.                                                                                          |
| project_1                   | keyword   | Used if more than one project level is allowed in the project hierarchy.                                      |
| project                     | keyword   | Project name.                                                                                                 |
| pull_request                | boolean   | True/False if the item is a pull request or not.                                                              |
| repository                  | keyword   | Repository name.                                                                                              |
| repository_labels           | keyword   | Custom repository labels defined by the user.                                                                 |
| state                       | keyword   | State of the item (open/closed).                                                                              |
| tag                         | keyword   | Perceval tag.                                                                                                 |
| time_open_days              | float     | Time the item is open, counted in days.                                                                       |
| time_to_close_days          | float     | Time to close an issue counted in days.                                                                       |
| time_to_first_attention     | float     | Time to first attention to an issue counted in days.                                                          |
| title_analyzed              | text      | Issue title split by terms to allow searching.                                                                |
| title                       | keyword   | The title of the issue.                                                                                       |
| updated_at                  | date      | Date when the issue was last updated.                                                                         |
| url_id                      | keyword   | Consists of the project path and the issue's id.                                                              |
| url                         | keyword   | Full URL of the issue.                                                                                        |
| user_data_bot               | boolean   | True/False if the user is a bot or not.                                                                       |
| user_data_domain            | keyword   | User's domain name from SortingHat profile.                                                                   |
| user_data_id                | keyword   | User's ID from SortingHat profile.                                                                            |
| user_data_name              | keyword   | User's name from SortingHat profile.                                                                          |
| user_data_org_name          | keyword   | Author's organization name from SortingHat profile.                                                           |
| user_data_multi_org_names   | keyword   | List of the author organizations from SortingHat profile.                                                     |
| user_data_user_name         | keyword   | User's username from SortingHat profile.                                                                      |
| user_data_uuid              | keyword   | User's UUID from SortingHat profile.                                                                          |
| user_domain                 | keyword   | User's domain name from GitHub.                                                                               |
| user_geolocation            | geo_point | User's global location using coordinates.                                                                     |
| user_location               | keyword   | User's geographical location.                                                                                 |
| user_login                  | keyword   | User's login name from GitHub.                                                                                |
| user_name                   | keyword   | User's name.                                                                                                  |
| user_org                    | keyword   | User's organization name.                                                                                     |
| uuid                        | keyword   | Perceval UUID.                                                                                                |
