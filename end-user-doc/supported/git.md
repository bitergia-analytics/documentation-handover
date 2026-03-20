# Git

Git is a software for tracking changes (version control system) in any set of
files, usually used for coordinating work among programmers collaboratively
developing source code during software development.


## Data from Git

### Commits

The documents in this index are about the commits of a Git repository. BAP has
information about the authors and committers of the commits. It can analyze the
commits and extracts the data about the authors who acknowledged, reported,
reviewed, and tested the commits. BAP can also analyze the pair programming
efforts of the authors.


## Data Model

The information for this data set is provided through indices in ElasticSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them it is available below.

| Index Pattern | Content |
| --- | --- |
| [git](../ref/datamodel/git.md) | Commits of the Git repository |
| [git_areas_of_code](../ref/datamodel/git_areas_of_code.md) | File modifications involved in each commit of the repository |
