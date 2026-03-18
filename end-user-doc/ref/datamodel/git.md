# Git Data Model

Documents in this index show information about commits of Git
repositories. Each document has the information for a Git commit
in a Git repository. All branches are tracked by default, in case
you want to filter in/out you will need the field `branches`.

The index names are in the format `git` or `git_enriched`.

All the field types are aggregatable except the `text` field type
(`message_analyzed`).

| **Name**                                     | **Type** | **Description**                                                                                                                      |
|----------------------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------|
| acked_by_multi_bots                          | boolean  | List of true if the given authors who acknowledged the commit, are identified as bots.                                               |
| acked_by_multi_domains                       | keyword  | List of domains associated with the authors in the SortingHat profile, who acknowledged the commit.                                  |
| acked_by_multi_names                         | keyword  | List of the author names, who acknowledged the commit.                                                                               |
| acked_by_multi_org_names                     | keyword  | List of the author organizations from the SortingHat profile, who acknowledged the commit.                                           |
| acked_by_multi_uuids                         | keyword  | List of the authors' UUID from SortingHat, who acknowledged the commit.                                                              |
| approved_by_multi_uuids                      | keyword  | List of the approvers' UUID from SortingHat.                                                                                         |
| author_bot                                   | boolean  | True if the given author is identified as a bot.                                                                                     |
| author_date                                  | date     | Date when the author made this commit.                                                                                               |
| author_date_hour                             | long     | Hour of the day when the author made this commit.                                                                                    |
| author_date_weekday                          | long     | Day of the week when the author made this commit.                                                                                    |
| author_domain                                | keyword  | Domain associated with the author in the SortingHat profile.                                                                         |
| author_gender (`disabled`)                   | keyword  | Author gender.                                                                                                                       |
| author_gender_acc (`disabled`)               | long     | Author gender accuracy.                                                                                                              |
| author_id                                    | keyword  | Author Id from SortingHat.                                                                                                           |
| author_multi_org_names                       | keyword  | List of the author organizations from SortingHat profile.                                                                            |
| author_name                                  | keyword  | Author name from SortingHat profile.                                                                                                 |
| author_org_name                              | keyword  | Author organization name from SortingHat profile.                                                                                    |
| author_user_name                             | keyword  | Author's username from SortingHat profile.                                                                                           |
| author_uuid                                  | keyword  | Author UUID from SortingHat.                                                                                                         |
| branches                                     | keyword  | List of branches where the commit appears. This field is empty by default, enable branches study in setup.cfg file.    |
| co_authored_by_multi_uuids                   | keyword  | List of co-authoring authors' UUID from SortingHat.                                                                                  |
| co_developed_by_multi_bots                   | boolean  | List of true if the given co-developed authors are identified as bots.                                                               |
| co_developed_by_multi_domains                | keyword  | List of domains associated with the co-developed authors in the SortingHat profile.                                                  |
| co_developed_by_multi_names                  | keyword  | List of co-developed authors' names.                                                                                                 |
| co_developed_by_multi_org_names              | keyword  | List of the co-developed author organizations from SortingHat profile.                                                               |
| co_developed_by_multi_uuids                  | keyword  | List of the co-developed authors' UUID from SortingHat.                                                                              |
| commit_date                                  | date     | Date when committer made this commit.                                                                                                |
| commit_date_hour                             | long     | Hour of the day when the committer made the commit.                                                                                  |
| commit_date_weekday                          | long     | Day of the week when the committer made the commit.                                                                                  |
| commit_tags                                  | keyword  | One or several tag(s) associated with the commit.                                                                                    |
| committer_domain                             | keyword  | Committer domain.                                                                                                                    |
| committer_name                               | keyword  | Committer name.                                                                                                                      |
| demography_max_date                          | date     | Date of the corresponding author's latest contribution (commit).                                                                     |
| demography_min_date                          | date     | Date of the corresponding author's first (oldest) contribution (commit).                                                             |
| files                                        | long     | Number of files touched by this commit.                                                                                              |
| git_author_domain                            | keyword  | Domain associated with the commit author in the SortingHat profile.                                                                  |
| git_uuid                                     | keyword  | Commit UUID.                                                                                                                         |
| github_repo                                  | keyword  | GitHub repository.                                                                                                                   |
| grimoire_creation_date                       | date     | Commit date (when the original author made the commit).                                                                              |
| hash                                         | keyword  | Commit hash.                                                                                                                         |
| hash_short                                   | keyword  | Shortened commit hash.                                                                                                               |
| is_git_commit                                | long     | Field containing '1' that allows to sum fields when concatenating with other indexes.                                                |
| lines_added                                  | long     | Number of lines added by this commit.                                                                                                |
| lines_changed                                | long     | Number of lines changed by this commit.                                                                                              |
| lines_removed                                | long     | Number of lines removed by this commit.                                                                                              |
| merged_by_multi_uuids                        | keyword  | List of the mergers' UUID from SortingHat.                                                                                           |
| message                                      | keyword  | Commit message as a single String.                                                                                                   |
| message_analyzed                             | text     | Commit message split by terms to allow searching.                                                                                    |
| metadata__enriched_on                        | date     | Date when the item was enriched.                                                                                                     |
| metadata__gelk_backend_name                  | keyword  | Name of the backend used to enrich information.                                                                                      |
| metadata__gelk_version                       | keyword  | Version of the backend used to enrich information.                                                                                   |
| metadata__timestamp                          | date     | Date when the item was stored in the RAW index.                                                                                      |
| metadata__updated_on                         | date     | Date when the item was updated in its original data source.                                                                          |
| non_authored_acked_by_multi_bots             | boolean  | List of true if the given authors are identified as bots who acknowledged the commit, excluding the commit author.                   |
| non_authored_acked_by_multi_domains          | keyword  | List of domains associated with the authors in the SortingHat profile who acknowledged the commit, excluding the commit author.      |
| non_authored_acked_by_multi_names            | keyword  | List of the authors' names who acknowledged the commit, excluding the commit author.                                                 |
| non_authored_acked_by_multi_org_names        | keyword  | List of the author organizations from the SortingHat profile who acknowledged the commit, excluding the commit author.               |
| non_authored_acked_by_multi_uuids            | keyword  | List of the authors' UUID from SortingHat profile who acknowledged the commit, excluding the commit author.                          |
| non_authored_approved_by_multi_uuids         | keyword  | List of the approvers' UUID from SortingHat, excluding the commit author.                                                            | 
| non_authored_co_authored_by_multi_uuids      | keyword  | List of the co-authoring authors' UUID from SortingHat, excluding the commit author.                                                 | 
| non_authored_co_developed_by_multi_bots      | boolean  | List of true if the given co-developed authors are identified as bots excluding the commit author.                                   |
| non_authored_co_developed_by_multi_domains   | keyword  | List of domains associated with the co-developed authors in SortingHat profile excluding the commit author.                          |
| non_authored_co_developed_by_multi_names     | keyword  | List of co-developed authors' names excluding the commit author.                                                                     |
| non_authored_co_developed_by_multi_org_names | keyword  | List of the co-developed author organizations from SortingHat profile excluding the commit author.                                   |
| non_authored_co_developed_by_multi_uuids     | keyword  | List of the co-developed authors UUID from SortingHat excluding the commit author.                                                   |
| non_authored_merged_by_multi_uuids           | keyword  | List of the mergers' UUID from SortingHat excluding the commit author.                                                               |
| non_authored_reported_by_multi_bots          | boolean  | List of true if the given reported authors are identified as bots excluding the commit author.                                       |
| non_authored_reported_by_multi_domains       | keyword  | List of domains associated with the reported authors in the SortingHat profile excluding the commit author.                          |
| non_authored_reported_by_multi_names         | keyword  | List of reported authors' names excluding the commit author.                                                                         |
| non_authored_reported_by_multi_org_names     | keyword  | List of the reported author organizations from SortingHat profile excluding the commit author.                                       |
| non_authored_reported_by_multi_uuids         | keyword  | List of the reported authors UUID from SortingHat excluding the commit author.                                                       |
| non_authored_reviewed_by_multi_bots          | boolean  | List of true if the given reviewed authors are identified as bots excluding the commit author.                                       |
| non_authored_reviewed_by_multi_domains       | keyword  | List of domains associated with the reviewed authors in the SortingHat profile excluding the commit author.                          |
| non_authored_reviewed_by_multi_names         | keyword  | List of reviewed authors' names excluding the commit author.                                                                         |
| non_authored_reviewed_by_multi_org_names     | keyword  | List of the reviewed author organizations from SortingHat profile excluding the commit author.                                       |
| non_authored_reviewed_by_multi_uuids         | keyword  | List of the reviewed authors UUID from SortingHat excluding the commit author.                                                       |
| non_authored_signed_off_by_multi_bots        | boolean  | List of true if the given signed-off authors are identified as bots excluding the commit author.                                     |
| non_authored_signed_off_by_multi_domains     | keyword  | List of domains associated with the signed-off authors in SortingHat profile excluding the commit author.                            |
| non_authored_signed_off_by_multi_names       | keyword  | List of signed-off authors' names excluding the commit author.                                                                       |
| non_authored_signed_off_by_multi_org_names   | keyword  | List of the signed-off author organizations from SortingHat profile excluding the commit author.                                     |
| non_authored_signed_off_by_multi_uuids       | keyword  | List of the signed-off authors UUID from SortingHat excluding the commit author.                                                     |
| non_authored_suggested_by_multi_bots         | boolean  | List of true if the given suggested authors are identified as bots excluding the commit author.                                      |
| non_authored_suggested_by_multi_domains      | keyword  | List of domains associated with the suggested authors in the SortingHat profile excluding the commit author.                         |
| non_authored_suggested_by_multi_names        | keyword  | List of suggested authors' names excluding the commit author.                                                                        |
| non_authored_suggested_by_multi_org_names    | keyword  | List of the suggested author organizations from SortingHat profile excluding the commit author.                                      |
| non_authored_suggested_by_multi_uuids        | keyword  | List of the suggested authors UUID from SortingHat excluding the commit author.                                                      |
| non_authored_tested_by_multi_bots            | boolean  | List of true if the given tested authors are identified as bots excluding the commit author.                                         |
| non_authored_tested_by_multi_domains         | keyword  | List of domains associated with the tested authors in the SortingHat profile excluding the commit author.                            |
| non_authored_tested_by_multi_names           | keyword  | List of tested authors' names excluding the commit author.                                                                           |
| non_authored_tested_by_multi_org_names       | keyword  | List of the tested author organizations from SortingHat profile excluding the commit author.                                         |
| non_authored_tested_by_multi_uuids           | keyword  | List of the tested authors UUID from SortingHat excluding the commit author.                                                         |
| origin                                       | keyword  | Original URL where the repository was retrieved from.                                                                                |
| painless_inverted_lines_removed_git          | long     | Number of lines removed per commit multiplied by -1.                                                                                 |
| project                                      | keyword  | Project.                                                                                                                             |
| project_1                                    | keyword  | Project (if more than one level is allowed in the project hierarchy).                                                                |
| repo_name                                    | keyword  | Repository name.                                                                                                                     |
| reported_by_multi_bots                       | boolean  | List of true if the given reported authors are identified as bots.                                                                   |
| reported_by_multi_domains                    | keyword  | List of domains associated with the reported authors in the SortingHat profile.                                                      |
| reported_by_multi_names                      | keyword  | List of reported authors' names.                                                                                                     |
| reported_by_multi_org_names                  | keyword  | List of the reported author organizations from the SortingHat profile.                                                               |
| reported_by_multi_uuids                      | keyword  | List of the reported authors' UUID from SortingHat.                                                                                  |
| repository_labels                            | keyword  | Custom repository labels defined by the user.                                                                                        |
| reviewed_by_multi_bots                       | boolean  | List of true if the given reviewed authors are identified as bots.                                                                   |
| reviewed_by_multi_domains                    | keyword  | List of domains associated with the reviewed authors in the SortingHat profile.                                                      |
| reviewed_by_multi_names                      | keyword  | List of reviewed authors' names.                                                                                                     |
| reviewed_by_multi_org_names                  | keyword  | List of the reviewed author organizations from SortingHat profile.                                                                   |
| reviewed_by_multi_uuids                      | keyword  | List of the reviewed authors' UUID from SortingHat.                                                                                  |
| signed_off_by_multi_bots                     | boolean  | List of true if the given signed-off authors are identified as bots.                                                                 |
| signed_off_by_multi_domains                  | keyword  | List of domains associated with the signed-off authors in the SortingHat profile.                                                    |
| signed_off_by_multi_names                    | keyword  | List of signed-off authors' names.                                                                                                   |
| signed_off_by_multi_org_names                | keyword  | List of the signed-off author organizations from SortingHat profile.                                                                 |
| signed_off_by_multi_uuids                    | keyword  | List of the signed-off authors' UUID from SortingHat.                                                                                |
| suggested_by_multi_bots                      | boolean  | List of true if the given suggested authors are identified as bots.                                                                  |
| suggested_by_multi_domains                   | keyword  | List of domains associated with the suggested authors in the SortingHat profile.                                                     |
| suggested_by_multi_names                     | keyword  | List of suggested authors' names.                                                                                                    |
| suggested_by_multi_org_names                 | keyword  | List of the suggested author organizations from the SortingHat profile.                                                              |
| suggested_by_multi_uuids                     | keyword  | List of the suggested authors' UUID from SortingHat.                                                                                 |
| tag                                          | keyword  | Perceval tag.                                                                                                                        |
| tested_by_multi_bots                         | boolean  | List of true if the given tested authors are identified as bots.                                                                     |
| tested_by_multi_domains                      | keyword  | List of domains associated with the tested authors in the SortingHat profile.                                                        |
| tested_by_multi_names                        | keyword  | List of tested authors' names.                                                                                                       |
| tested_by_multi_org_names                    | keyword  | List of the tested author organizations from SortingHat profile.                                                                     |
| tested_by_multi_uuids                        | keyword  | List of the tested authors' UUID from SortingHat.                                                                                    |
| time_to_commit_hours                         | long     | Time in hours from author_date (when the commit was originally created) to commit date (when the commit was made to the repository). |
| title                                        | keyword  | Commit title.                                                                                                                        |
| tz                                           | long     | Timezone in which the commit was made by its original author.                                                                        |
| utc_author                                   | date     | Author date (when the original author made the commit) in UTC.                                                                       |
| utc_author_hour                              | date     | Hour of the day when the author made the commit in UTC.                                                                              |
| utc_author_weekday                           | long     | Day of the week when the author made the commit in UTC.                                                                              |
| utc_commit                                   | date     | Commit date in UTC.                                                                                                                  |
| utc_commit_hour                              | date     | Hour of the day when the committer made the commit in UTC.                                                                           |
| utc_commit_weekday                           | long     | Day of the week when the committer made the commit in UTC.                                                                           |
| uuid                                         | keyword  | Perceval UUID.                                                                                                                       |
