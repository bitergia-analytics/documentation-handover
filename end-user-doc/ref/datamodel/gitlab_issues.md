# GitLab Issues Data Model

Documents in this index are about the issues of a GitLab project.

All the field types are aggregatable except the `text` field type
(`title_analyzed`).

| **Name**                    | **Type** | **Description**                                                                                                                           |
|-----------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------|
| assignee_bot                | boolean  | True if the given assignee is identified as a bot.                                                                                        |
| assignee_domain             | keyword  | Domain associated to the assignee in SortingHat profile.                                                                                  |
| assignee_gender             | keyword  | Assignee gender, based on her name (disabled by default).                                                                                 |
| assignee_gender_acc         | long     | Assignee gender accuracy (disabled by default).                                                                                           |
| assignee_id                 | keyword  | Assignee Id from SortingHat.                                                                                                              |
| assignee_multi_org_names    | keyword  | List of the assignee organizations from SortingHat profile.                                                                               |
| assignee_name               | keyword  | Assignee name.                                                                                                                            |
| assignee_org_name           | keyword  | Assignee organization name.                                                                                                               |
| assignee_user_name          | keyword  | Assignee user name from SortingHat.                                                                                                       |
| assignee_username           | keyword  | Assignee user name from GitLab.                                                                                                           |
| assignee_uuid               | keyword  | Assignee UUID from SortingHat.                                                                                                            |
| author_bot                  | boolean  | True if the given author is identified as a bot.                                                                                          |
| author_domain               | keyword  | Domain associated with the author in the SortingHat profile.                                                                              |
| author_gender               | keyword  | Author gender, based on her name (disabled by default).                                                                                   |
| author_gender_acc           | long     | Author gender accuracy (disabled by default).                                                                                             |
| author_id                   | keyword  | Author Id from SortingHat.                                                                                                                |
| author_multi_org_names      | keyword  | List of the author organizations from SortingHat profile.                                                                                 |
| author_name                 | keyword  | Author name.                                                                                                                              |
| author_org_name             | keyword  | Author organization name.                                                                                                                 |
| author_user_name            | keyword  | Author user name from SortingHat.                                                                                                         |
| author_username             | keyword  | Author user name from GitLab.                                                                                                             |
| author_uuid                 | keyword  | Author UUID from SortingHat.                                                                                                              |
| closed_at                   | date     | Date in which the Issue was closed.                                                                                                       |
| created_at                  | date     | Date in which the Issue was created.                                                                                                      |
| gitlab_repo                 | keyword  | GitLab repository name.                                                                                                                   |
| grimoire_creation_date      | date     | Issue creation date.                                                                                                                      |
| id                          | long     | Issue Id in GitLab.                                                                                                                       |
| id_in_repo                  | long     | Issue Id in the repository it belongs to.                                                                                                 |
| is_gitlab_issue             | long     | 1 indicating this is an Issue, used for counting in case other kind of items could be stored in the same index or alias.                  |
| labels                      | keyword  | Issue assigned labels.                                                                                                                    |
| metadata__enriched_on       | date     | Date when the item was enriched.                                                                                                          |
| metadata__gelk_backend_name | keyword  | Name of the backend used to enrich information.                                                                                           |
| metadata__gelk_version      | keyword  | Version of the backend used to enrich information.                                                                                        |
| metadata__timestamp         | date     | Date when the item was stored in the RAW index.                                                                                           |
| metadata__updated_on        | date     | Date when the item was updated on its original data source.                                                                               |
| milestone                   | keyword  | Assigned milestone.                                                                                                                       |
| milestone_due_date          | date     | Date when a milestone was due.                                                                                                            |
| milestone_id                | long     | Id of the milestone, unique for all GitLab.                                                                                               |
| milestone_iid               | long     | Id of the milestone, unique for the GitLab repository.                                                                                    |
| milestone_start_date        | date     | Date when a milestone was started.                                                                                                        |
| milestone_url               | keyword  | URL of the milestone.                                                                                                                     |
| origin                      | keyword  | Original URL where the repository was retrieved from.                                                                                     |
| painless_time_open          | float    | Real-time open days.                                                                                                                      |
| project                     | keyword  | Project.                                                                                                                                  |
| project_1                   | keyword  | Project (if more than one level is allowed in project hierarchy).                                                                         |
| repository                  | keyword  | Repository name.                                                                                                                          |
| repository_labels           | keyword  | Custom repository labels defined by the user.                                                                                             |
| state                       | keyword  | 'opened' or 'closed'.                                                                                                                     |
| tag                         | keyword  | Perceval tag.                                                                                                                             |
| time_open_days              | float    | Time open in days.                                                                                                                        |
| time_to_close_days          | float    | Time to close Issue in days.                                                                                                              |
| time_to_first_attention     | float    | Time from creation to first comment or reaction (whatever occurs first) added by an author different from the one who created this Issue. |
| title                       | keyword  | Issue title.                                                                                                                              |
| title_analyzed              | text     | Issue title split by terms to allow searching.                                                                                            |
| updated_at                  | date     | Date when the Issue was updated.                                                                                                          |
| url                         | keyword  | Issue URL.                                                                                                                                |
| url_id                      | keyword  | Consist of project path and Issue id in that project.                                                                                     |
| uuid                        | keyword  | Perceval UUID.                                                                                                                            |
