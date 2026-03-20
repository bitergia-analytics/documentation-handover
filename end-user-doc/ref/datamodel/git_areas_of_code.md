# Git Areas of Code Data Model

Documents in this index are about the file modifications involved in each commit
of the Git repository. That means we can have more than a document per commit.

The index names are in the format `git_aoc` or `git_areas_of_code`.

All the field types are aggregatable except the `text` field type (`message`).

| **Name**                       | **Type** | **Description**                                                                                |
|--------------------------------|----------|------------------------------------------------------------------------------------------------|
| addedlines                     | long     | Number of lines added in this file by this commit (only in this file, not the whole commit).   |
| author_bot                     | boolean  | True if the given author is identified as a bot.                                               |
| author_domain                  | keyword  | Domain associated with the author in the SortingHat profile.                                   |
| author_id                      | keyword  | Author Id from SortingHat.                                                                     |
| author_multi_org_names         | keyword  | List of the author organizations from SortingHat profile.                                      |
| author_name                    | keyword  | Author name.                                                                                   |
| author_org_name                | keyword  | Organization name.                                                                             |
| author_user_name               | keyword  | Author user name.                                                                              |
| author_uuid                    | keyword  | Author UUID from SortingHat.                                                                   |
| committer                      | keyword  | Committer name as it appears in commit (including e-mail).                                     |
| committer_date                 | date     | Date when committer made this commit.                                                          |
| date                           | date     | Author date (when the original author made the commit).                                        |
| eventtype                      | keyword  | Event type. In Git AOC, it is 'COMMIT'.                                                        |
| file_dir_name                  | keyword  | Path in which the file is located, not including file name.                                    |
| file_ext                       | keyword  | File extension.                                                                                |
| file_name                      | keyword  | Filename with extension.                                                                       |
| file_path_list                 | keyword  | List of split path parts.                                                                      |
| fileaction                     | keyword  | Action performed by the commit over the file.                                                  |
| filepath                       | keyword  | Complete file path.                                                                            |
| files                          | long     | Number of files touched by the same commit this file is included in.                           |
| filetype                       | keyword  | Code or Other, based on file extension.                                                        |
| git_author_domain              | keyword  | Domain extracted from author email included within the commit, if any.                         |
| grimoire_creation_date         | date     | Author date (when the original author made the commit).                                        |
| hash                           | keyword  | Commit hash.                                                                                   |
| id                             | keyword  | Commit hash.                                                                                   |
| message                        | text     | Commit message split by terms.                                                                 |
| message.keyword                | keyword  | Commit message as a single String.                                                             |
| metadata__enriched_on          | date     | Date when the item was enriched.                                                               |
| metadata__timestamp            | date     | Date when the item was stored in the RAW index.                                                |
| metadata__updated_on           | date     | Date when the item was updated in its original data source.                                    |
| origin                         | keyword  | Original URL where the repository was retrieved from.                                          |
| owner                          | keyword  | Owner (code author) name as it appears in commit (including e-mail).                           |
| painless_inverted_removedlines | long     | Number of lines removed per file multiplied by -1.                                             |
| perceval_uuid                  | keyword  | Perceval UUID.                                                                                 |
| project                        | keyword  | Project.                                                                                       |
| project_1                      | keyword  | Project (if more than one level is allowed in the project hierarchy).                          |
| removedlines                   | long     | Number of lines removed in this file by this commit (only in this file, not the whole commit). |
| repository                     | keyword  | Repository name.                                                                               |
| uuid                           | keyword  | Item unique identifier.                                                                        |
