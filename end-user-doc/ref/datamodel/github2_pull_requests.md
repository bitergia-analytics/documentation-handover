# GitHub Pull Requests Comments Data Model

## Warnings and Disclaimers

On one hand, Github treats internally the pull requests as issues, and this causes
misleading field names and misunderstandings.

On the other hand the capability of crossing information from different datasets by
the search engine Bitergia Analytics platform bases on is very limited. Thus we need
to create mixed datasets and this again causes misunderstandings. This data source is
one of these cases.

## Physical Design Approach of this Data Source

This index contains 3 kind of documents related to Github pull requests.
It is possible to distinguish them by using the field `item_type`: ( `issue`, `pull_request`, `comment`).

There's one document of type `comment` per pull request comment plus 2 other documents per GitHub pull request, an `issue` and a `pull_request`.

There are also 2 subtypes of documents of type `comment` depending on the value of their `subtype` field: `issue_comment` or `review_comment`.

All the field types are aggregatable except the `text` field type. Those are:

  - `title_analyzed`.
  - `issue_title_analyzed`.
  - `body_analyzed`.

## Fields Description

|     provenance | icon                          |
|----------------|-------------------------------|
|         `issue`| 🎫                            |
|  `pull_request`| 🤞                            |
| `issue_comment`| 🗣️                            |
|`review_comment`| 🔍                            |      
|      SortingHat| 🎩                            |
|    common field| 📎                            |


| **Name**                       | **Type**  | **Description**                                                                                                      | provenance |
|--------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------|------------|
| _Cross-references fields_      | NA        | Fields coming from cross-references study (available only when it is active), see [cross_references.csv](https://github.com/chaoss/grimoirelab-elk/blob/master/schema/cross_references.csv).              |     |
| assignee_data_bot              | boolean   | True/False if the pull request assignee is a bot or not                                                              | 🎩 |
| assignee_data_domain           | keyword   | Pull request assignee domain name.                                                                                   | 🎩 |
| assignee_data_gender           | keyword   | Pull request assignee gender, based on her name (disabled by default).                                               | 🎩 |
| assignee_data_gender_acc       | float     | Pull request assignee gender accuracy (disabled by default).                                                         | 🎩 |
| assignee_data_id               | keyword   | Pull request assignee SortingHat profile ID.                                                                         | 🎩 |
| assignee_data_name             | keyword   | Pull request assignee name.                                                                                          | 🎩 |
| assignee_data_multi_org_names  | list      | Pull request assignee organization names.                                                                            | 🎩 |
| assignee_data_org_name         | keyword   | Pull request assignee organization name.                                                                             | 🎩 |
| assignee_data_user_name        | keyword   | Pull request assignee username.                                                                                      | 🎩 |
| assignee_data_uuid             | keyword   | Pull request assignee SortingHat profile UUID.                                                                       | 🎩 |
| assignee_domain                | keyword   | Pull request assignee domain name from GitHub.                                                                       | 🎫 |
| assignee_geolocation           | geo_point | Pull request assignee geolocation from GitHub.                                                                       | 🎫 |
| assignee_location              | keyword   | Pull request assignee location from GitHub.                                                                          | 🎫 |
| assignee_login                 | keyword   | Pull request assignee login from GitHub.                                                                             | 🎫 |
| assignee_name                  | keyword   | Pull request assignee name from GitHub.                                                                              | 🎫 |
| assignee_org                   | keyword   | Pull request assignee organization name from Github.                                                                 | 🎫 |
| author_bot                     | boolean   | True/False if the pull request author is a bot or not from the SortingHat profile.                                   | 🎩 |
| author_domain                  | keyword   | Item (Pull request or comment) author domain name from SortingHat profile.                                           | 🎩 |
| author_gender                  | keyword   | Item (Pull request or comment) author gender, based on her name, from SortingHat (disabled by default).              | 🎩 |
| author_gender_acc              | float     | Item (Pull request or comment) author gender accuracy from SortingHat (disabled by default).                         | 🎩 |
| author_id                      | keyword   | Item (Pull request or comment) author SortingHat profile ID.                                                         | 🎩 |
| author_multi_org_names         | list      | Item (Pull request or comment) author organization names from SortingHat profile.                                    | 🎩 |
| author_name                    | keyword   | Item (Pull request or comment) author name from SortingHat profile.                                                  | 🎩 |
| author_org_name                | keyword   | Item (Pull request or comment) author organization name from SortingHat profile.                                     | 🎩 |
| author_user_name               | keyword   | Item (Pull request or comment) author username from SortingHat profile.                                              | 🎩 |
| author_uuid                    | keyword   | Item (Pull request or comment) author SortingHat profile UUID.                                                       | 🎩 |
| body                           | keyword   | Body of the comment.                                                                                                 | 🔍 🗣️ |
| body_analyzed                  | text      | Body of the comment.                                                                                                 | 🔍 🗣️ |
| code_merge_duration            | float     | Difference in days between creation and merging dates.                                                               | 🤞             |
| comment_created_at             | date      | Date when the comment was created.                                                                                   | 🗣️ |
| comment_updated_at             | date      | Date when the comment was updated.                                                                                   | 🔍 🗣️ |
| demography_max_date            | date      | Date of the latest pull request of the corresponding author. Available only when demography study is active.         | ? |
| demography_min_date            | date      | Date of the first (oldest) pull request of the corresponding author. Available only when demography study is active. | ? |
| forks                          | long      | Number of repository forks.                                                                                          | 🤞             |
| github_repo                    | keyword   | GitHub repository name.                                                                                              | 🎫 🤞  🔍 🗣️ |
| grimoire_creation_date         | date      | Pull request/comment creation date.                                                                                  | 📎 |
| id                             | keyword   | Pull request/comment ID. Different id's for 🎫 vs 🤞                                            | 🎫 🤞 🔍 🗣️ |
| is_github_comment              | long      | Used to identify or count (any) **comments**.                                                                        | 🔍 🗣️ |
| is_github_pull_request         | long      | Used to identify or count `pull_request` items.                                                                      | 🤞             |
| is_github_review_comment       | long      | Used to identify or count **review comments**. 1 for them.                                                           | 🔍 |
| is_github_issue_comment        | long      | Used to identify or count **issue comments**. 1 for them.                                                            | 🗣️ |
| issue_id_in_repo               | keyword   | Original identifier of the pull request (GitHub pull request number).                                                | 🎫 🤞 🔍 🗣️ |
| issue_closed_at                | date      | Date in which the pull request was closed.                                                                           | 🎫 🗣️ |
| issue_created_at               | date      | Date in which the pull request was created.                                                                          | 🎫 🗣️ |
| issue_labels                   | list      | Labels of the pull request.                                                                                          | 🎫 🗣️ |
| issue_pull_request             | boolean   | True for documents of subtype `issue_comment`.                                                                       | 🗣️ |
| issue_state                    | keyword   | Life cycle state of the related pull request.                                                                        | 🗣️ |
| issue_title                    | keyword   | Title of the related pull request for documents of type `comment`.                                                   | 🤞 🔍 🗣️ |
| issue_updated_at               | date      | Date when the pull request was last updated.                                                                         | 🗣️ |
| issue_url                      | keyword   | URL of the pull request for documents of type `comment`.                                                             | 🔍 🗣️ |
| item_type                      | keyword   | The type of the item (`issue`, `pull_request`, `comment`).                                                           | 🎫 🤞 🔍 🗣️ |
| merge_author_domain            | keyword   | Merge author domain from GitHub.                                                                                     | 🔍 |
| merge_author_geolocation       | geo_point | Merge author geolocation from GitHub.                                                                                | 🔍 |
| merge_author_location          | keyword   | Merge author location as string from GitHub.                                                                         | 🔍 |
| merge_author_login             | keyword   | Merge author login from GitHub.                                                                                      | 🔍 |
| merge_author_name              | keyword   | Merge author name from GitHub.                                                                                       | 🔍 |
| merge_author_org               | keyword   | Merge author organization from GitHub.                                                                               | 🔍 |
| merged_by_data_bot             | boolean   | True/False if the merge author is a bot or not                                                                       | 🎩 |
| merged_by_data_domain          | keyword   | Merge author domain.                                                                                                 | 🎩 |
| merged_by_data_gender          | keyword   | Merge author gender, based on her name (disabled by default).                                                        | 🎩 |
| merged_by_data_gender_acc      | float     | Merge author gender accuracy (disabled by default).                                                                  | 🎩 |
| merged_by_data_id              | keyword   | Merge author's SortingHat profile ID.                                                                                | 🎩 |
| merged_by_data_name            | keyword   | Merge author name.                                                                                                   | 🎩 |
| merged_by_data_org_name        | keyword   | Merge author organization.                                                                                           | 🎩 |
| merged_by_data_user_name       | keyword   | Merge author username.                                                                                               | 🎩 |
| merged_by_data_uuid            | keyword   | Merge author SortingHat profile UUID.                                                                                | 🎩 |
| metadata__enriched_on          | date      | Date when the item was enriched.                                                                                     | 📎|
| metadata__gelk_backend_name    | keyword   | Name of the backend used to enrich information.                                                                      | 📎|
| metadata__gelk_version         | keyword   | Version of the backend used to enrich information.                                                                   | 📎|
| metadata__timestamp            | date      | Date when the item was stored in the RAW index.                                                                      | 📎|
| metadata__updated_on           | date      | Date when the item was updated on its original data source.                                                          | 📎|
| num_review_comments            | long      | Number of review comments.                                                                                           | 🤞             |
| offset                         | long      |                                                                                                                      | 📎|
| origin                         | keyword   | Original URL of the repository the document was retrieved from.                                                      | 📎|
| project                        | keyword   | Project.                                                                                                             | 📎|
| project_1                      | keyword   | Project (if more than one level is allowed in the project hierarchy).                                                | 📎|
| pull_id_in_repo                | keyword   | Original identifier of the pull request (GitHub pull request number).                                                | 🤞 🔍       |
| pull_closed_at                 | date      | Date in which the pull request was closed.                                                                           | 🤞 🔍       |
| pull_created_at                | date      | Date in which the pull request was created.                                                                          | 🤞 🔍       |
| pull_id                        | keyword   | Pull request ID on GitHub.                                                                                           | 🤞 🔍       |
| pull_id_in_repo                | keyword   | Pull request ID in the GitHub repository.                                                                            | 🤞 🔍       |
| pull_labels                    | keyword   | Pull request assigned labels.                                                                                        | 🤞 🔍       |
| pull_merged                    | boolean   | True if the pull request was already merged.                                                                         | 🤞 🔍 |
| pull_merged_at                 | date      | Date when the pull request was merged.                                                                               | 🤞 🔍 |
| pull_state                     | keyword   | Life cycle state of the pull request (`open`/`closed`/`merged`).                                                     | 🤞 🔍 |
| pull_updated_at                | date      | Date when the pull request was last updated.                                                                         | 🤞 🔍 |
| pull_url                       | keyword   | Full URL of the pull request.                                                                      .                 | 🤞 🔍 |
| reaction_confused              | long      | Number of reactions 'confused'.                                                                                      | 🎫 🗣️ 🔍 |
| reaction_eyes                  | long      | Number of reactions 'eyes'.                                                                                          | 🎫 🗣️ 🔍 |
| reaction_heart                 | long      | Number of reactions 'heart'.                                                                                         | 🎫 🗣️ 🔍 |
| reaction_hooray                | long      | Number of reactions 'hooray'.                                                                                        | 🎫 🗣️ 🔍 |
| reaction_rocket                | long      | Number of reactions 'rocket'.                                                                                        | 🎫 🗣️ 🔍 |
| reaction_thumb_down            | long      | Number of reactions '-1'.                                                                                            | 🎫 🗣️ 🔍 |
| reaction_thumb_up              | long      | Number of reactions '+1'.                                                                                            | 🎫 🗣️ 🔍 |
| reaction_total_count           | long      | Number of total reactions.                                                                                           | 🎫 🗣️ 🔍 |
| repository                     | keyword   | Repository URL.                                                                                                      | 📎 |
| repository_labels              | keyword   | Custom repository labels defined by the user.                                                                        | 📎 |
| review_state                   | keyword   | Review lifecycle state (`APPROVED`, `COMMENTED`, `CHANGES_REQUESTED` , or empty).                                    |🔍 |
| sub_type                       | keyword   | Type of the comment (`issue_comment` or `review_comment`).                                                           | 🗣️ 🔍 |
| tag                            | keyword   | Perceval tag. (The URL of the repository).                                                                           | 📎 |
| time_open_days                 | float     | Time the pull request is open counted in days.                                                                       | 🎫 🤞    |
| time_to_close_days             | float     | Time to close a pull request counted in days.                                                                        | 🎫 🤞    |
| time_to_merge_request_response | float     | Time to merge a pull request in days.                                                                                | 🤞             |
| url                            | keyword   | Url of the pull request/comment. The `issue` and its corresponding `pull_request` share url. Each comment has its own. | 🎫 🤞  🗣️ 🔍 |
| user_data_bot                  | boolean   | True/False if the pull request author is a bot or not.                                                               | 🎩 |
| user_data_domain               | keyword   | Pull request author domain name.                                                                                     | 🎩 |
| user_data_gender               | keyword   | Pull Request author gender, based on her name (disabled by default).                                                 | 🎩 |
| user_data_gender_acc           | float     | Pull request author gender accuracy (disabled by default).                                                           | 🎩 |
| user_data_id                   | keyword   | Pull request author SortingHat profile ID.                                                                           | 🎩 |
| user_data_name                 | keyword   | Pull request author name.                                                                                            | 🎩 |
| user_data_org_name             | keyword   | Pull request author organization name.                                                                               | 🎩 |
| user_data_user_name            | keyword   | Pull request author username.                                                                                        | 🎩 |
| user_data_uuid                 | keyword   | Pull request author SortingHat profile UUID.                                                                         | 🎩 |
| user_domain                    | keyword   | Pull request author domain name from GitHub.                                                                         | 🎫 🤞    |
| user_geolocation               | geo_point | Pull request author geolocation from GitHub.                                                                         | 🎫 🤞    |
| user_location                  | keyword   | Pull request author location as string from GitHub.                                                                  | 🎫 🤞    |
| user_login                     | keyword   | Pull request author login from GitHub.                                                                               | 🎫 🤞  🗣️ 🔍 |
| user_name                      | keyword   | Pull request author username from GitHub.                                                                            | 🎫 🤞    |
| user_org                       | keyword   | Pull request author organization from GitHub.                                                                        | 🎫 🤞    |
| uuid                           | keyword   | Perceval UUID. Different for each item.                                                                              | 📎 |
