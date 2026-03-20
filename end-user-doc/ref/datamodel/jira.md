# Jira Data Model

Documents in this index are either about a Jira issue or an issue comment. It is
possible to distinguish the different document types by using the field `type`.

All the field types are aggregatable except the `text` field type. Those are

  - `body`
  - `main_description_analyzed`

> Note: Some fields might be disabled (`disabled` tag is mentioned). This field can be
> enabled [updating the setup.cfg file](../../mordred_configuration.md#configuration-file).

| **Name**                             | **Type** | **Description**                                                          |
|--------------------------------------|----------|--------------------------------------------------------------------------|
| assignee                             | keyword  | Assignee of the issue.                                                   |
| assignee_bot                         | boolean  | True/False if the assignee is a bot or not.                              |
| assignee_domain                      | keyword  | Assignee's domain name from SortingHat profile.                          |
| assignee_gender (`disabled`)         | keyword  | Assignee gender.                                                         |
| assignee_gender_acc (`disabled`)     | long     | Assignee gender accuracy.                                                |
| assignee_id                          | keyword  | Assignee's id from SortingHat profile.                                   |
| assignee_multi_org_names             | keyword  | List of the assignee organizations from the SortingHat profile.          |
| assignee_name                        | keyword  | Assignee's name.                                                         |
| assignee_org_name                    | keyword  | Assignee organization name.                                              |
| assignee_tz                          | keyword  | Assignee's timezone.                                                     |
| assignee_user_name                   | keyword  | Assignee's username from SortingHat profile.                             |
| assignee_uuid                        | keyword  | Assignee's UUID from SortingHat profile.                                 |
| author                               | keyword  | Author of the issue/comment.                                             |
| author_bot                           | boolean  | True/False if the author is a bot or not.                                |
| author_domain                        | keyword  | Author's domain name from SortingHat profile.                            |
| author_gender (`disabled`)           | keyword  | Author gender.                                                           |
| author_gender_acc (`disabled`)       | long     | Author gender accuracy.                                                  |
| author_id                            | keyword  | Author's id from SortingHat profile.                                     |
| author_login                         | keyword  | Author's login name from Jira.                                           |
| author_multi_org_names               | keyword  | List of the author organizations from SortingHat profile.                |
| author_name                          | keyword  | Author's name.                                                           |
| author_org_name                      | keyword  | Author organization name.                                                |
| author_type                          | keyword  | Type of Author.                                                          |
| author_tz                            | keyword  | Author's timezone.                                                       |
| author_user_name                     | keyword  | Author's username from SortingHat profile.                               |
| author_uuid                          | keyword  | Author's UUID from SortingHat profile.                                   |
| body                                 | text     | Body of the issue comment.                                               |
| changes                              | long     | Number of changes in the issue.                                          |
| comment_id                           | keyword  | Id of the comment of the Jira issue.                                     |
| created                              | date     | Date when an issue was opened.                                           |
| creation_date                        | date     | Date when the comment was posted.                                        |
| creator_bot                          | boolean  | True/False if the creator of the issue is a bot or not.                  |
| creator_domain                       | keyword  | Creator's domain name from SortingHat profile.                           |
| creator_gender (`disabled`)          | keyword  | Creator gender.                                                          |
| creator_gender_acc (`disabled`)      | long     | Creator gender accuracy.                                                 |
| creator_id                           | keyword  | Creator's id from SortingHat profile.                                    |
| creator_login                        | keyword  | Creator's login from SortingHat profile.                                 |
| creator_multi_org_names              | keyword  | List of the creator organizations from SortingHat profile.               |
| creator_name                         | keyword  | Creator's name.                                                          |
| creator_org_name                     | keyword  | Creator organization name.                                               |
| creator_tz                           | keyword  | Creator's timezone.                                                      |
| creator_user_name                    | keyword  | Creator's username from SortingHat profile.                              |
| creator_uuid                         | keyword  | Creator's UUID from SortingHat profile.                                  |
| grimoire_creation_date               | date     | Issue creation date.                                                     |
| id                                   | keyword  | Issue/Comment Id in Jira.                                                |
| is_closed                            | long     | Flag to check if the issue is closed or not.                             |
| is_jira_comment                      | long     | Flag to check if the item is an issue comment in Jira                    |
| is_jira_issue                        | long     | Flag to check if the item is an issue in Jira                            |
| issue_description                    | keyword  | Description of the Issue type in Jira.                                   |
| issue_key                            | keyword  | Issue Id for a Jira comment.                                             |
| issue_type                           | keyword  | Type of Issue (Bug/Story/Task).                                          |
| issue_url                            | keyword  | Issue URL for a Jira comment.                                            |
| key                                  | keyword  | Issue Id of the Jira issue.                                              |
| labels                               | keyword  | Labels of the issue in Jira.                                             |
| main_description                     | keyword  | Description of the Issue in Jira.                                        |
| main_description_analyzed            | text     | Description of the Issue in Jira.                                        |
| metadata__enriched_on                | date     | Date when the data were enriched.                                        |
| metadata__gelk_backend_name          | keyword  | Name of the backend used to enrich the data.                             |
| metadata__gelk_version               | keyword  | Version of the backend used to enrich the data.                          |
| metadata__timestamp                  | date     | Date when the item was stored in ElasticSearch raw index.                |
| metadata__updated_on                 | date     | Date when the item was updated on its original data source.              |
| number_of_comments                   | long     | Number of comments to the issue in Jira.                                 |
| origin                               | keyword  | The original URL from which the repository was retrieved.                |
| original_time_estimation             | long     | Time estimation for the issue (in seconds).                              |
| original_time_estimation_hours       | ling     | Time estimation for the issue (in hours).                                |
| painless_delay                       | float    | Real-time open (in days).                                                |
| painless_time_to_now                 | float    | Duration between now and `grimoire_creation_date` (in days).             |
| priority                             | keyword  | Priority of the issue.                                                   |
| progress_total                       | long     | Total progress of the issue.                                             |
| project                              | keyword  | Project name.                                                            |
| project_1                            | keyword  | Used if more than one project level is allowed in the project hierarchy. |
| project_id                           | keyword  | Id of the project.                                                       |
| project_key                          | keyword  | Key assigned to the project.                                             |
| project_name                         | keyword  | Name of the project.                                                     |
| reporter_bot                         | boolean  | True/False if the reporter of the issue is a bot or not.                 |
| reporter_domain                      | keyword  | Reporter's domain name from SortingHat profile.                          |
| reporter_gender (`disabled`)         | keyword  | Reporter gender.                                                         |
| reporter_gender_acc (`disabled`)     | long     | Reporter gender accuracy.                                                |
| reporter_id                          | keyword  | Reporter's id from SortingHat profile.                                   |
| reporter_login                       | keyword  | Reporter's login from SortingHat profile.                                |
| reporter_multi_org_names             | keyword  | List of the reporter organizations from the SortingHat profile.          |
| reporter_name                        | keyword  | Reporter's name.                                                         |
| reporter_org_name                    | keyword  | Reporter organization name.                                              |
| reporter_tz                          | keyword  | Reporter's timezone.                                                     |
| reporter_user_name                   | keyword  | Reporter's username from SortingHat profile.                             |
| reporter_uuid                        | keyword  | Reporter's UUID from SortingHat profile.                                 |
| resolution_date                      | date     | Date of the Resolution.                                                  |
| resolution_description               | keyword  | Description of the Resolution.                                           |
| resolution_id                        | keyword  | Id of the Resolution.                                                    |
| resolution_name                      | keyword  | Name of the Resolution.                                                  |
| resolution_self                      | keyword  | REST URL of the Resolution.                                              |
| status                               | keyword  | Status of the issue (Resolved/Open/To Do, etc.).                         |
| status_category_key                  | keyword  | Key assigned to status of the issue.                                     |
| status_description                   | keyword  | Description of the status of the issue.                                  |
| summary                              | keyword  | Title of the issue.                                                      |
| tag                                  | keyword  | Perceval tag.                                                            |
| time_estimation                      | long     | Time estimation for completing the issue (in seconds).                   |
| time_estimation_hours                | long     | Time estimation for completing the issue (in hours).                     |
| time_spent                           | long     | Time spent for completing the issue (in seconds).                        |
| time_spent_hours                     | float    | Time spent for completing the issue (in hours).                          |
| time_to_close_days                   | float    | Time taken to close the issue (in days).                                 |
| time_to_last_update_days             | float    | Time since there was an update on the issue (in days).                   |
| type                                 | keyword  | The type of the item (issue/comment).                                    |
| updateAuthor                         | keyword  | Author of the comment updated in the issue.                              |
| updateAuthor_bot                     | boolean  | True/False if the author is a bot or not.                                |
| updateAuthor_domain                  | keyword  | Author's domain name from SortingHat profile.                            |
| updateAuthor_gender (`disabled`)     | keyword  | Author gender.                                                           |
| updateAuthor_gender_acc (`disabled`) | long     | Author gender accuracy.                                                  |
| updateAuthor_id                      | keyword  | Author's id from SortingHat profile.                                     |
| updateAuthor_multi_org_names         | keyword  | List of the author organizations from SortingHat profile.                |
| updateAuthor_name                    | keyword  | Author's name.                                                           |
| updateAuthor_org_name                | keyword  | Author organization name.                                                |
| updateAuthor_tz                      | keyword  | Author's timezone.                                                       |
| updateAuthor_user_name               | keyword  | Author's username from SortingHat profile.                               |
| updateAuthor_uuid                    | keyword  | Author's UUID from SortingHat profile.                                   |
| updated                              | date     | Date when the Issue was updated.                                         |
| url                                  | keyword  | Issue URL.                                                               |
| uuid                                 | keyword  | Perceval UUID.                                                           |
| watchers                             | long     | Number of watchers for the issue.                                        |
