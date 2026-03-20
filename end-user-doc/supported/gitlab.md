# GitLab

GitLab is a repository hosting manager tool that is developed by GitLab Inc and
is used for the software development process. It provides a variety of
management by which we can streamline our collaborative workflow for completing
the software development lifecycle.


## Data from GitLab

### Commits

The documents in this index are about the commit logs of a GitLab repository.
You can know more information about the data from the [Git data
source](git.md#commits).

### Issues

The documents in this index are about the collaboration and coordination
happening on GitLab Issues. BAP has the information about the full lifecycle of
an issue from when it was opened to when it was closed. BAP can analyze the data
of the contributors who opened the issue, who closed it, and who was assigned to
it. It analyzes how labels are added & removed and about the milestones to
understand the workflow issues go through. Our platform can also calculate time
taken for first comment or reaction added by another contributor/maintainer
other than the person who opened the issue.

### Merge Requests

The documents in this index are about the collaboration and coordination
happening on GitLab Merge Requests. BAP has information about the full lifecycle
of an merge request from when it was opened to when it was merged/closed. Our
platform can analyze the data of the contributors who opened the merge request,
and the maintainers who closed/merged it. It analyzes how labels are added &
removed to understand the workflow merge requests go through. BAP can also
calculate the time in days, and when was the merge request was open/closed.


## Data Model

The information for this data set is provided through indices in ElasticSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them it is available below.

| Index Pattern | Content |
| --- | --- |
| [git](../ref/datamodel/git.md) | Commits of the GitLab repository |
| [git_areas_of_code](../ref/datamodel/git_areas_of_code.md) | File modifications involved in each commit of the repository |
| [gitlab_issues](../ref/datamodel/gitlab_issues.md) | Issues of a GitLab project, one issue per document |
| [gitlab_merge_requests](../ref/datamodel/gitlab_merge_requests.md) | Merge requests of a GitLab project, one merge request per document |

## Tracking private repositories

Issues, merge request and commits can be tracked for private repositories on GitLab.
To do so, one of our mining accounts must be added to the organization
containing the private repositories. Once added, we will have access to the private
repositories and we will generate an OAuth token to collect their data.

The data extracted from private repositories does not receive any special processing.
Thus, the information shown on the dashboard will be the same of the one of public
repos (e.g., commit messages and hashes, file paths, issue comments).
