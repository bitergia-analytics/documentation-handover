# GitHub Events Data Model

This index contains one document per GitHub event. It is possible to distinguish
them by using the field `event_type`.

All the field types are aggregatable except the `text` field type. Those are:

  - `title_analyzed`.
  - `issue_title_analyzed`.
  - `body_analyzed`.

| **Name**                     | **Type** | **Description**                                                                                         |
| ---------------------------- | -------- | ------------------------------------------------------------------------------------------------------- |
| _Cross-references fields_    | NA       | Fields coming from cross references study (available only when it is active), see [cross_references.csv](https://github.com/chaoss/grimoirelab-elk/blob/master/schema/cross_references.csv). |
| actor_bot                    | boolean  | True/False if the event actor is a bot or not from SortingHat profile.                                  |
| actor_domain                 | keyword  | Event actor domain name from SortingHat profile.                                                        |
| actor_gender                 | keyword  | Event actor gender, based on her name, from SortingHat (disabled by default).                           |
| actor_gender_acc             | float    | Event actor gender accuracy from SortingHat (disabled by default).                                      |
| actor_id                     | keyword  | Event actor ID from SortingHat profile.                                                                 |
| actor_name                   | keyword  | Event actor name from SortingHat profile.                                                               |
| actor_org_name               | keyword  | Event actor organization name from SortingHat profile.                                                  |
| actor_multi_org_names        | keyword  | List of the actor organizations from SortingHat profile.                                                |
| actor_user_name              | keyword  | Event actor username from SortingHat profile.                                                           |
| actor_uuid                   | keyword  | Event actor UUID from SortingHat profile.                                                               |
| author_bot                   | boolean  | True/False if the event author is a bot or not from SortingHat profile.                                 |
| author_domain                | keyword  | Event actor domain name from SortingHat profile.                                                        |
| author_gender                | keyword  | Event actor gender, based on her name, from SortingHat (disabled by default).                           |
| author_gender_acc            | float    | Event actor gender accuracy from SortingHat (disabled by default).                                      |
| author_id                    | keyword  | Event actor ID from SortingHat profile.                                                                 |
| author_name                  | keyword  | Event actor name from SortingHat profile.                                                               |
| author_org_name              | keyword  | Event actor organization name from SortingHat profile.                                                  |
| author_multi_org_names       | keyword  | List of the actor organizations from SortingHat profile.                                                |
| author_user_name             | keyword  | Event actor username from SortingHat profile.                                                           |
| author_uuid                  | keyword  | Event actor UUID from SortingHat profile.                                                               |
| board_closed_at              | date     | Date when the board was closed.                                                                         |
| board_column                 | keyword  | Name of the column where the issue is.                                                                  |
| board_created_at             | date     | Date when the board was created.                                                                        |
| board_name                   | keyword  | Name of the board.                                                                                      |
| board_previous_column        | keyword  | Name of the previous column where the issue was.                                                        |
| board_state                  | keyword  | State of the board (open/closed).                                                                       |
| board_updated_at             | date     | Date when the board was updated.                                                                        |
| board_url                    | keyword  | URL of the board.                                                                                       |
| closer_closed                | boolean  | True/False if the pull request is closed or not.                                                        |
| closer_closed_at             | date     | Date when the pull request was closed.                                                                  |
| closer_created_at            | date     | Date when the pull request was created.                                                                 |
| closer_event_url             | keyword  | URL where the closed event occurred.                                                                    |
| closer_event_url             | boolean  | True/False if the pull request is merged or not.                                                        |
| closer_number                | long     | Number of the pull request.                                                                             |
| closer_pull_submitter        | keyword  | Pull request submitter login.                                                                           |
| closer_repo                  | keyword  | Repository of the pull request.                                                                         |
| closer_type                  | keyword  | Type of the closer object (currently only pull requests are processed).                                 |
| closer_updated_at            | date     | Date when the pull request was updated.                                                                 |
| closer_url                   | keyword  | URL of the pull request.                                                                                |
| created_at                   | date     | Date when the event was created.                                                                        |
| duration_from_previous_event | long     | Duration in days from the previous event (added by duration analysis study).                            |
| event_type                   | keyword  | Type of the event processed.                                                                            |
| github_repo                  | keyword  | GitHub repository name of the issue.                                                                    |
| grimoire_creation_date       | date     | Pull Request creation date.                                                                             |
| is_github_issue              | long     | Used to separate issues from other items such as pull requests.                                         |
| issue_closed_at              | date     | Date when the issue was closed.                                                                         |
| issue_created_at             | date     | Date when the issue was opened.                                                                         |
| issue_id                     | long     | Issue's ID in GitHub.                                                                                   |
| id_in_repo                   | keyword  | The issue's ID in the repository it was created.                                                        |
| issue_labels                 | keyword  | The labels assigned to an issue.                                                                        |
| issue_state                  | keyword  | State of the item (open/closed).                                                                        |
| issue_updated_at             | date     | Date when the issue was last updated.                                                                   |
| issue_url_id                 | keyword  | Consists of the project path and the issue's id.                                                        |
| issue_url                    | keyword  | Full URL of the issue.                                                                                  |
| item_type                    | keyword  | The type of the item (issue/pull request).                                                              |
| label                        | keyword  | Label name.                                                                                             |
| label_description            | keyword  | Label description.                                                                                      |
| label_created_at             | date     | Date when the label was created.                                                                        |
| label_is_default             | boolean  | True/False whether the label is a GitHub default one.                                                   |
| label_updated_at             | date     | Date when the label was updated.                                                                        |
| merge_closed                 | boolean  | True/False if the pull request is closed or not.                                                        |
| merge_closed_at              | date     | Date when the pull request was closed.                                                                  |
| merge_created_at             | date     | Date when the pull request was created.                                                                 |
| merge_merged                 | boolean  | True/False if the pull request is merged or not.                                                        |
| merge_merged_at              | date     | Date when the pull request was merged.                                                                  |
| merge_updated_at             | date     | Date when the pull request was updated.                                                                 |
| merge_url                    | string   | URL of the pull request.                                                                                |
| metadata__enriched_on        | date     | Date when the data were enriched.                                                                       |
| metadata__gelk_backend_name  | keyword  | Name of the backend used to enrich the data.                                                            |
| metadata__gelk_version       | keyword  | Version of the backend used to enrich the data.                                                         |
| metadata__timestamp          | date     | Date when the item was stored in ElasticSearch raw index.                                               |
| metadata__updated_on         | date     | Date when the item was updated on its original data source.                                             |
| origin                       | keyword  | The original URL from which the repository was retrieved from.                                          |
| previous_event_uuid          | keyword  | Previous event uuid (added by duration analysis study).                                                 |
| project_1                    | keyword  | Used if more than one project levels are allowed in the project hierarchy.                              |
| project                      | keyword  | Project name.                                                                                           |
| pull_request                 | boolean  | True/False if the item is a pull request or not.                                                        |
| reference_will_close_target  | boolean  | True/False if the target will be closed when the source is merged.                                      |
| reference_cross_repo         | boolean  | True/False if the reference originated in a different repository.                                       |
| reference_event_url          | keyword  | URL of the reference event.                                                                             |
| reference_source_closed      | boolean  | True/False if the source is closed or not.                                                              |
| reference_source_closed_at   | date     | Date when the source was closed.                                                                        |
| reference_source_created_at  | date     | Date when the source was created.                                                                       |
| reference_source_merged      | boolean  | True/False if the source was merged or not.                                                             |
| reference_source_number      | long     | Number of the source.                                                                                   |
| reference_source_repo        | keyword  | Repo of the source.                                                                                     |
| reference_source_type        | keyword  | Type of the source (issue/pull request).                                                                |
| reference_source_updated_at  | date     | Date when the source was updated.                                                                       |
| reference_source_url         | keyword  | URL of the source.                                                                                      |
| reporter_bot                 | boolean  | True/False if the issue reporter is a bot or not from SortingHat profile.                               |
| reporter_domain              | keyword  | Issue reporter domain name from SortingHat profile.                                                     |
| reporter_gender              | keyword  | Issue reporter gender, based on her name, from SortingHat (disabled by default).                        |
| reporter_gender_acc          | float    | Issue reporter gender accuracy from SortingHat (disabled by default).                                   |
| reporter_id                  | keyword  | Issue reporter ID from SortingHat profile.                                                              |
| reporter_name                | keyword  | Issue reporter name from SortingHat profile.                                                            |
| reporter_org_name            | keyword  | Issue reporter organization name from SortingHat profile.                                               |
| reporter_multi_org_names     | keyword  | List of the reporter organizations from SortingHat profile.                                             |
| reporter_user_name           | keyword  | Issue reporter username from SortingHat profile.                                                        |
| reporter_uuid                | keyword  | Issue reporter UUID from SortingHat profile.                                                            |
| repository                   | keyword  | Repository name.                                                                                        |
| repository_labels            | keyword  | Custom repository labels defined by the user.                                                           |
| submitter_bot                | boolean  | True/False if the pull request submitter is a bot or not from SortingHat profile.                       |
| submitter_domain             | keyword  | Pull request submitter domain name from SortingHat profile.                                             |
| submitter_gender             | keyword  | Pull request submitter gender, based on her name, from SortingHat (disabled by default).                |
| submitter_gender_acc         | float    | Pull request submitter gender accuracy from SortingHat (disabled by default).                           |
| submitter_id                 | keyword  | Pull request submitter ID from SortingHat profile.                                                      |
| submitter_name               | keyword  | Pull request submitter name from SortingHat profile.                                                    |
| submitter_org_name           | keyword  | Pull request submitter organization name from SortingHat profile.                                       |
| submitter_multi_org_names    | keyword  | List of the pull request submitter organizations from SortingHat profile.                               |
| submitter_user_name          | keyword  | Pull request submitter username from SortingHat profile.                                                |
| submitter_uuid               | keyword  | Pull request submitter UUID from SortingHat profile.                                                    |
| tag                          | keyword  | Perceval tag.                                                                                           |
| title                        | keyword  | The title of the Pull Request.                                                                          |
| title_analyzed               | text     | Pull Request title split by terms to allow searching.                                                   |
| uuid                         | keyword  | Perceval UUID.                                                                                          |
