# GitHub Issue Comments Data Model

This index contains one document per GitHub issue or an issue comment. It is
possible to distinguish them by using the field `item_type`.

All the field types are aggregatable except the `text` field type. Those are:

  - `title_analyzed`.
  - `issue_title_analyzed`.
  - `body_analyzed`.

| **Name**                    | **Type**  | **Description**                                                                                               |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------|
| _Cross-references fields_   | NA        | Fields coming from cross-references study (available only when it is active), see [cross_references.csv](https://github.com/chaoss/grimoirelab-elk/blob/master/schema/cross_references.csv).       |
| assignee_data_bot           | boolean   | True/False if the assignee is a bot or not.                                                                   |
| assignee_data_domain        | keyword   | Assignee's domain name from SortingHat profile.                                                               |
| assignee_data_gender        | keyword   | Assignee gender.                                                                                              |
| assignee_data_gender_acc    | keyword   | Accuracy to assess assignee gender.                                                                           |
| assignee_data_id            | keyword   | Assignee's id from SortingHat profile.                                                                        |
| assignee_data_name          | keyword   | Assignee's name.                                                                                              |
| assignee_data_org_name      | keyword   | Assignee's organization name from SortingHat profile.                                                         |
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
| author_gender               | keyword   | Author gender.                                                                                                |
| author_gender_acc           | keyword   | Accuracy to assess author gender.                                                                             |
| author_id                   | keyword   | Author's ID from SortingHat profile.                                                                          |
| author_name                 | keyword   | Author's name.                                                                                                |
| author_org_name             | keyword   | Author's organization name from SortingHat profile.                                                           |
| author_user_name            | keyword   | Author's username from SortingHat profile.                                                                    |
| author_uuid                 | keyword   | Author's UUID from SortingHat profile.                                                                        |
| body                        | keyword   | Body of the issue/comment.                                                                                    |
| body_analyzed               | text      | Body of the issue/comment.                                                                                    |
| comment_updated_at          | date      | Date when the comment was updated.                                                                            |
| demography_max_date         | date      | Date of the latest issue of the corresponding author. Available only when demography study is active.         |
| demography_min_date         | date      | Date of the first (oldest) issue of the corresponding author. Available only when demography study is active. |
| feeling_emoticon            | keyword   |                                                                                                               |
| feeling_emoticon_sentiment  | keyword   |                                                                                                               |
| github_repo                 | keyword   | The name of the GitHub repository.                                                                            |
| grimoire_creation_date      | date      | Issue/comment creation date.                                                                                  |
| id                          | keyword   | Issue/comment ID.                                                                                             |
| is_github_issue             | long      | Used to separate issues from comments.                                                                        |
| is_github_issue_comment     | long      | Used to separate comments from issues.                                                                        |
| is_github_comment           | long      | Used to unify pull requests and issue comments.                                                               |
| issue_closed_at             | date      | Date when an issue was closed.                                                                                |
| issue_created_at            | date      | Date when an issue was opened.                                                                                |
| issue_id                    | long      | Issue ID on GitHub.                                                                                           |
| issue_id_in_repo            | keyword   | The issue's ID in the repository.                                                                             |
| issue_labels                | keyword   | The labels assigned to an issue.                                                                              |
| issue_pull_request          | boolean   | True if the issue is a pull request.                                                                          |
| issue_state                 | keyword   | State of the issue (open/closed).                                                                             |
| issue_updated_at            | date      | Date when the issue was last updated.                                                                         |
| issue_url                   | keyword   | Full URL of the issue.                                                                                        |
| item_type                   | keyword   | The type of the item (issue/comment).                                                                         |
| metadata__enriched_on       | date      | Date when the data were enriched.                                                                             |
| metadata__gelk_backend_name | keyword   | Name of the backend used to enrich the data.                                                                  |
| metadata__gelk_version      | keyword   | Version of the backend used to enrich the data.                                                               |
| metadata__timestamp         | date      | Date when the item was stored in ElasticSearch raw index.                                                     |
| metadata__updated_on        | date      | Date when the item was updated on its original data source.                                                   |
| origin                      | keyword   | The original URL from which the repository was retrieved.                                                     |
| project_1                   | keyword   | Used if more than one project level is allowed in the project hierarchy.                                      |
| project                     | keyword   | Project name.                                                                                                 |
| reaction_confused           | long      | Number of reactions 'confused'.                                                                               |
| reaction_eyes               | long      | Number of reactions 'eyes'.                                                                                   |
| reaction_heart              | long      | Number of reactions 'heart'.                                                                                  |
| reaction_hooray             | long      | Number of reactions 'hooray'.                                                                                 |
| reaction_rocket             | long      | Number of reactions 'rocket'.                                                                                 |
| reaction_thumb_down         | long      | Number of reactions '-1'.                                                                                     |
| reaction_thumb_up           | long      | Number of reactions '+1'.                                                                                     |
| reaction_total_count        | long      | Number of total reactions.                                                                                    |
| repository                  | keyword   | Repository name.                                                                                              |
| repository_labels           | keyword   | Custom repository labels defined by the user.                                                                 |
| sub_type                    | keyword   | Type of the comment (issue comment).                                                                          |
| tag                         | keyword   | Perceval tag.                                                                                                 |
| time_open_days              | float     | Time the item is open, counted in days.                                                                       |
| time_to_close_days          | float     | Time to close an issue counted in days.                                                                       |
| time_to_first_attention     | float     | Time to first attention to an issue counted in days.                                                          |
| issue_title_analyzed        | text      | Issue title split by terms to allow searching.                                                                |
| issue_title                 | keyword   | The title of the issue.                                                                                       |
| url                         | keyword   | Url of the issue/comment.                                                                                     |
| user_data_bot               | boolean   | True/False if the user is a bot or not.                                                                       |
| user_data_domain            | keyword   | User's domain name from SortingHat profile.                                                                   |
| user_data_gender            | keyword   | User gender.                                                                                                  |
| user_data_gender_acc        | keyword   | Accuracy to assess user gender.                                                                               |
| user_data_id                | keyword   | User's ID from SortingHat profile.                                                                            |
| user_data_name              | keyword   | User's name from SortingHat profile.                                                                          |
| user_data_org_name          | keyword   | User's organization name from SortingHat profile.                                                             |
| user_data_user_name         | keyword   | User's username from SortingHat profile.                                                                      |
| user_data_uuid              | keyword   | User's UUID from SortingHat profile.                                                                          |
| user_domain                 | keyword   | User's domain name from GitHub.                                                                               |
| user_geolocation            | geo_point | User's global location using coordinates.                                                                     |
| user_location               | keyword   | User's geographical location.                                                                                 |
| user_login                  | keyword   | User's login name from GitHub.                                                                                |
| user_name                   | keyword   | User's name.                                                                                                  |
| user_org                    | keyword   | User's organization name.                                                                                     |
| uuid                        | keyword   | Perceval UUID.                                                                                                |
