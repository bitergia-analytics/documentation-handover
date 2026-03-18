# GitHub Repositories Data Model

This index contains one document per GitHub repository.

| **Name**                    | **Type** | **Description**                                                                  |
|-----------------------------|----------|----------------------------------------------------------------------------------|
| fetched_on                  | long     | Timestamp when the item was fetched, equivalent to metadata__updated_on.         |
| forks_count                 | long     | Number of forks of the repository.                                               |
| grimoire_creation_date      | date     | Date when the repo was fetched.                                                  |
| is_github_repository        | long     | Used to separate repositories from other items such as pull requests and issues. |
| metadata__enriched_on       | date     | Date when the data were enriched.                                                |
| metadata__gelk_backend_name | keyword  | Name of the backend used to enrich the data.                                     |
| metadata__gelk_version      | keyword  | Version of the backend used to enrich the data.                                  |
| metadata__timestamp         | date     | Date when the item was stored in ElasticSearch raw index.                        |
| metadata__updated_on        | date     | Date when the item was updated on its original data source.                      |
| origin                      | keyword  | The original URL from which the repository was retrieved.                        |
| repository_labels           | keyword  | Custom repository labels defined by the user.                                    |
| stargazers_count            | long     | Number of stars of the repository.                                               |
| subscribers_count           | long     | Number of watchers of the repository.                                            |
| tag                         | keyword  | Perceval tag.                                                                    |
| url                         | keyword  | Full URL of the repository                                                       |
| uuid                        | keyword  | Perceval UUID.                                                                   |
