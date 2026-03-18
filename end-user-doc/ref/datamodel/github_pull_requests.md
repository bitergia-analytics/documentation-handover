# GitHub Pull Requests Data Model

This index contains one document per GitHub pull request.

All the field types are aggregatable except the `text` field type. Those are:

  - `title_analyzed`.
  - `issue_title_analyzed`.
  - `body_analyzed`.

| **Name**                       | **Type**  | **Description**                                                                                                                    |
|--------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| _Cross-references fields_      | NA        | Fields coming from cross-references study (available only when it is active), see [cross_references.csv](https://github.com/chaoss/grimoirelab-elk/blob/master/schema/cross_references.csv).                            |
| additions                      | long      | Number of additions in the Pull Request.                                                                                           |
| assignee_geolocation           | geo_point | Pull Request assignee geolocation from GitHub.                                                                                     |
| author_bot                     | boolean   | True/False if the Pull Request author is a bot or not from the SortingHat profile.                                                 |
| author_domain                  | keyword   | Pull Request author domain name from SortingHat profile.                                                                           |
| author_gender                  | keyword   | Pull Request author gender, based on her name, from SortingHat (disabled by default).                                              |
| author_gender_acc              | float     | Pull Request author gender accuracy from SortingHat (disabled by default).                                                         |
| author_id                      | keyword   | Pull Request author ID from SortingHat profile.                                                                                    |
| author_name                    | keyword   | Pull Request author name from SortingHat profile.                                                                                  |
| author_org_name                | keyword   | Pull Request author organization name from SortingHat profile.                                                                     |
| author_multi_org_names         | keyword   | List of the author organizations from SortingHat profile.                                                                          |
| author_user_name               | keyword   | Pull Request author username from SortingHat profile.                                                                              |
| author_uuid                    | keyword   | Pull Request author UUID from SortingHat profile.                                                                                  |
| changed_files                  | long      | Number of changed files in the Pull Request.                                                                                       |
| closed_at                      | date      | Date in which the Issue was closed.                                                                                                |
| code_merge_duration            | float     | Difference in days between creation and merging dates.                                                                             |
| created_at                     | date      | Date in which the Issue was created.                                                                                               |
| deletions                      | long      | Number of deletions in the Pull Request.                                                                                           |
| forks                          | long      | Number of repository forks.                                                                                                        |
| github_repo                    | keyword   | GitHub repository name.                                                                                                            |
| grimoire_creation_date         | date      | Pull Request creation date.                                                                                                        |
| id                             | long      | ID in GitHub.                                                                                                                      |
| id_in_repo                     | keyword   | ID in the GitHub repository it was created.                                                                                        |
| issue_url                      | keyword   | Full URL of the issue.                                                                                                             |
| is_github_pull_request         | long      | 1 indicating this is a Pull Request, used for counting in case other kinds of items could be stored in the same index or alias.    |
| item_type                      | keyword   | Item type, in this case, `pull_request`. In old BAP versions (< 0.33) the underscore was missing and was `pull request`.                                             |
| labels                         | keyword   | Pull Request assigned labels.                                                                                                      |
| merge_author_domain            | keyword   | Merge author domain from GitHub.                                                                                                   |
| merge_author_geolocation       | geo_point | Merge author geolocation from GitHub.                                                                                              |
| merge_author_location          | keyword   | Merge author location as string from GitHub.                                                                                       |
| merge_author_login             | keyword   | Merge author login from GitHub.                                                                                                    |
| merge_author_name              | keyword   | Merge author name from GitHub.                                                                                                     |
| merge_author_org               | keyword   | Merge author organization from GitHub.                                                                                             |
| merged                         | boolean   | True if the Pull Request was already merged.                                                                                       |
| merged_at                      | date      | Date when the Pull Request was merged.                                                                                             |
| merged_by_data_bot             | boolean   | True/False if the merge author is a bot or not, from SortingHat profile.                                                           |
| merged_by_data_domain          | keyword   | Merge author domain from SortingHat profile.                                                                                       |
| merged_by_data_gender          | keyword   | Merge author gender, based on her name, from SortingHat profile(disabled by default).                                              |
| merged_by_data_gender_acc      | float     | Merge author gender accuracy from SortingHat profile(disabled by default).                                                         |
| merged_by_data_id              | keyword   | Merge author's ID from SortingHat profile.                                                                                         |
| merged_by_data_name            | keyword   | Merge author name from SortingHat profile.                                                                                         |
| merged_by_data_org_name        | keyword   | Merge author organization from SortingHat profile.                                                                                 |
| merged_by_multi_org_names      | keyword   | List of the merge author organizations from the SortingHat profile.                                                                |
| merged_by_data_user_name       | keyword   | Merge author username from SortingHat profile.                                                                                     |
| merged_by_data_uuid            | keyword   | Merge author UUID from SortingHat profile.                                                                                         |
| metadata__enriched_on          | date      | Date when the item was enriched.                                                                                                   |
| metadata__gelk_backend_name    | keyword   | Name of the backend used to enrich information.                                                                                    |
| metadata__gelk_version         | keyword   | Version of the backend used to enrich information.                                                                                 |
| metadata__timestamp            | date      | Date when the item was stored in the RAW index.                                                                                    |
| metadata__updated_on           | date      | Date when the item was updated on its original data source.                                                                        |
| num_review_comments            | long      | Number of comments.                                                                                                                |
| origin                         | keyword   | Original URL where the repository was retrieved from.                                                                              |
| project                        | keyword   | Project.                                                                                                                           |
| project_1                      | keyword   | Project (if more than one level is allowed in the project hierarchy).                                                              |
| pull_request                   | boolean   | True indicating this item is a pull request or not (to be used when the index is queried through aliases including other indexes). |
| repository                     | keyword   | Repository name.                                                                                                                   |
| repository_labels              | keyword   | Custom repository labels defined by the user.                                                                                      |
| state                          | keyword   | State of the Pull Request (GitHub has only 2 possible states: open or closed).                                                     |
| tag                            | keyword   | Perceval tag.                                                                                                                      |
| time_open_days                 | float     | Time the Pull Request is open, counted in days.                                                                                    |
| time_to_close_days             | float     | Time to close a Pull Request counted in days.                                                                                      |
| time_to_merge_request_response | float     | Time to get a response on a Pull Request in days.                                                                                  |
| title                          | keyword   | The title of the Pull Request.                                                                                                     |
| title_analyzed                 | text      | Pull Request title split by terms to allow searching.                                                                              |
| updated_at                     | date      | Date when the Pull Request was last updated.                                                                                       |
| url                            | keyword   | Full URL of the Pull Request.                                                                                                      |
| url_id                         | keyword   | Consists of the project path and the Pull Request id.                                                                              |
| user_data_bot                  | boolean   | True/False if the Pull Request author is a bot or not from the SortingHat profile.                                                 |
| user_data_domain               | keyword   | Pull Request author domain name from SortingHat profile.                                                                           |
| user_data_gender               | keyword   | Pull Request author gender, based on her name, from SortingHat (disabled by default).                                              |
| user_data_gender_acc           | float     | Pull Request author gender accuracy from SortingHat (disabled by default).                                                         |
| user_data_id                   | keyword   | Pull Request author ID from SortingHat profile.                                                                                    |
| user_data_name                 | keyword   | Pull Request author name from SortingHat profile.                                                                                  |
| user_data_org_name             | keyword   | Pull Request author organization name from SortingHat profile.                                                                     |
| user_data_multi_org_names      | keyword   | List of the Pull Request author organizations from SortingHat profile.                                                             |
| user_data_user_name            | keyword   | Pull Request author username from SortingHat profile.                                                                              |
| user_data_uuid                 | keyword   | Pull Request author UUID from SortingHat profile.                                                                                  |
| user_domain                    | keyword   | Pull Request author domain name from GitHub.                                                                                       |
| user_geolocation               | geo_point | Pull Request author geolocation from GitHub.                                                                                       |
| user_location                  | keyword   | Pull Request author location as string from GitHub.                                                                                |
| user_login                     | keyword   | Pull Request author login from GitHub.                                                                                             |
| user_name                      | keyword   | Pull Request author username from GitHub.                                                                                          |
| user_org                       | keyword   | Pull Request author organization from GitHub.                                                                                      |
| uuid                           | keyword   | Perceval UUID.                                                                                                                     |
