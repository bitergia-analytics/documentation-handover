# Stack Overflow Data Model

This index contains one document per Stack Exchange question or an answer. It is
possible to distinguish them by using the field `type`.

All the field types are aggregatable except the `text` field type
(`title_analyzed`).

> Note:
>
>   - Some fields might be deprecated (`deprecated` tag is mentioned). It is
>     advised not to use the deprecated fields.


| **Name**                       | **Type** | **Description**                                                          |
|--------------------------------|----------|--------------------------------------------------------------------------|
| answer_count                   | long     | Number of answers to the question.                                       |
| answer_id                      | long     | Id of the answer.                                                        |
| answer_status                  | keyword  | Status of the answer (accepted/not_accepted).                            |
| answer_tags (`deprecated`)     | keyword  | Tags of the answer.                                                      |
| answers_tags (`deprecated`)    | keyword  | Tags of the answers per question.                                        |
| author                         | keyword  | Author of the question/answer.                                           |
| author_bot                     | boolean  | True/False if the author is a bot or not.                                |
| author_domain                  | keyword  | Author's domain name from SortingHat profile.                            |
| author_gender (`disabled`)     | keyword  | Author gender.                                                           |
| author_gender_acc (`disabled`) | long     | Author gender accuracy.                                                  |
| author_id                      | keyword  | Author's ID from SortingHat profile.                                     |
| author_link                    | keyword  | Profile link of the author.                                              |
| author_multi_org_names         | keyword  | List of the author organizations from SortingHat profile.                |
| author_name                    | keyword  | Author's name from SortingHat profile.                                   |
| author_org_name                | keyword  | Author's organization name from SortingHat profile.                      |
| author_reputation              | long     | Reputation of the author.                                                |
| author_user_name               | keyword  | Author's username from SortingHat profile.                               |
| author_uuid                    | keyword  | Author's UUID from SortingHat profile.                                   |
| comment_count                  | long     | Number of comments on the question/answer.                               |
| creation_date                  | date     | Date when the question/answer is created.                                |
| delete_vote_count              | long     | Number of people who voted to delete the question.                       |
| down_vote_count                | long     | Number of people who down-voted the question/answer.                     |
| favorite_count                 | long     | Number of people who marked the question as favorite.                    |
| grimoire_creation_date         | date     | Date when the question/answer is created.                                |
| is_accepted                    | boolean  | True/False if the answer is accepted.                                    |
| is_accepted_answer             | long     | True/False if the answer is accepted.                                    |
| is_stackexchange_answer        | long     | Used to separate answers from questions.                                 |
| is_stackexchange_question      | long     | Used to separate questions from answers.                                 |
| item_id                        | long     | Id of the question/answer.                                               |
| last_activity_date             | long     | Date of the recent activity on the question/answer.                      |
| link                           | keyword  | URL of the question/answer.                                              |
| metadata__enriched_on          | date     | Date when the data were enriched.                                        |
| metadata__gelk_backend_name    | keyword  | Name of the backend used to enrich the data.                             |
| metadata__gelk_version         | keyword  | Version of the backend used to enrich the data.                          |
| metadata__timestamp            | date     | Date when the item was stored in ElasticSearch raw index.                |
| metadata__updated_on           | date     | Date when the item was updated on its original data source.              |
| origin                         | keyword  | The original URL from which the repository was retrieved.                |
| owner_bot                      | boolean  | True/False if the owner is a bot or not.                                 |
| owner_domain                   | keyword  | Owner's domain name from SortingHat profile.                             |
| owner_gender (`disabled`)      | keyword  | Owner gender.                                                            |
| owner_gender_acc (`disabled`)  | long     | Owner gender accuracy.                                                   |
| owner_id                       | keyword  | Owner's ID from SortingHat profile.                                      |
| owner_multi_org_names          | keyword  | List of the owner organizations from SortingHat profile.                 |
| owner_name                     | keyword  | Owner's name.                                                            |
| owner_org_name                 | keyword  | Owner's organization name from SortingHat profile.                       |
| owner_user_name                | keyword  | Owner's username from SortingHat profile.                                |
| owner_uuid                     | keyword  | Owner's UUID from SortingHat profile.                                    |
| project                        | keyword  | Project name.                                                            |
| project_1                      | keyword  | Used if more than one project level is allowed in the project hierarchy. |
| question_accepted_answer_id    | long     | Id of the answer accepted for the question.                              |
| question_has_accepted_answer   | boolean  | True/False if the question has an accepted answer.                       |
| question_id                    | long     | Id of the question.                                                      |
| question_tags                  | keyword  | Tags of the question.                                                    |
| question_title                 | keyword  | Title of the question.                                                   |
| repository_labels              | keyword  | Custom repository labels defined by the user.                            |
| reputation (`deprecated`)      | keyword  | Reputation score of the author.                                          |
| score                          | long     | Score of the question/answer.                                            |
| tag                            | keyword  | Perceval tag.                                                            |
| tags                           | keyword  | Tags of the question.                                                    |
| thread_tags (`deprecated`)     | keyword  | Combined list of tags of question and answers, per question.             |
| title                          | keyword  | Title of the question.                                                   |
| title_analyzed                 | text     | Title of the question split by terms to allow searching.                 |
| type                           | keyword  | The type of the item (question/answer).                                  |
| up_vote_count                  | long     | Number of people who up-voted the question/answer.                       |
| uuid                           | keyword  | Perceval UUID.                                                           |
| view_count                     | long     | Number of views of the question.                                         |
