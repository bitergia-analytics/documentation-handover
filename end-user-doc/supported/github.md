# GitHub

GitHub is a code hosting platform for version control and collaboration. It lets
you and others work together on projects from anywhere. It is an increasingly
popular programming resource used for code sharing. It's a social networking
site for programmers that many companies and organizations use to facilitate
project management and collaboration.


## Data from GitHub

### Commits

The documents in this index are about the commit logs of a GitHub repository.
You can know more information about the data from the [Git data
source](git.md#commits).

### Issues and Comments

The documents in this index are about the collaboration and coordination
happening on GitHub Issues. BAP has the  information about the full lifecycle of
an issue from when it was opened to when it was closed. BAP can analyze the data
of the contributors who opened the issue, who closed it, who commented on
the issues, and who was assigned to it. It analyzes how labels are added &
removed and the milestones to understand the workflow issues go through.
Bitergia also calculates time taken for first comment or reaction added by
another contributor/maintainer other than the person who opened the issue. BAP
also analyzes the comments and reactions data of the comments in the issues.

### Pull Requests and Comments

The documents in this index are about the collaboration and coordination
happening on GitHub Pull Requests. BAP has the information about the full
lifecycle of an pull request from when it was opened to when it was
merged/closed. You can analyze the data of the contributors who opened the pull
request, who commented & reviewed the changes, and the maintainers who
closed/merged it. BAP calculates the time in days, the merge request was
open/closed. It also analyzes the comments and reactions data of the comments in
the merge requests.

### Repository Statistics

The documents in this index are about the GitHub Repository Statistics. BAP
analyzes the statistics such as number of forks, stargazers and subscribers of
the github repository.

### Events

The documents in this index are about the GitHub Events. Bitergia tracks the
data of events such as commit event, gollum event, issue event, issue comment
event, push event, release event, etc. of a github repository. You can read more
about [github events
types](https://docs.github.com/en/developers/webhooks-and-events/events/github-event-types).


## Data Model

The information for this data set is provided through indices in ElasticSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them it is available below.

| Index Pattern | Content |
| --- | --- |
| [git](../ref/datamodel/git.md) | Commits of the GitHub repository |
| [git_areas_of_code](../ref/datamodel/git_areas_of_code.md) | File modifications involved in each commit of the repository |
| [github_events](../ref/datamodel/github_events.md) | GitHub event, it is possible to distinguish them by using the field `event_type` |
| [github_issues](../ref/datamodel/github_issues.md) | GitHub issues and pull requests |
| [github_pull_requests](../ref/datamodel/github_pull_requests.md) | Github pull requests, one per document |
| [github_repos](../ref/datamodel/github_repos.md) | Basic stats for GitHub repositories, one per document |
| [github2_issues](../ref/datamodel/github2_issues.md) | One document per GitHub issue or issue comment |
| [github2_pull_requests](../ref/datamodel/github2_pull_requests.md) | One document per pull request or comment |

## Tracking private repositories

Issues, pull requests and commits can be tracked for private repositories on GitHub.
To do so, one of our mining accounts must be added to the organization
containing the private repositories. Once added, we will have access to the private
repositories and we will generate an OAuth token to collect their data.

The data extracted from private repositories does not receive any special processing.
Thus, the information shown on the dashboard will be the same of the one of public
repos (e.g., commit messages and hashes, file paths, issue comments).
