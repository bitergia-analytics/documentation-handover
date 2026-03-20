# Bugzilla

Bugzilla is a popular open-source bug tracking system used to manage and track software
defects. It provides a centralized platform for developers, testers, and project managers
to report, assign, and resolve issues.

## Data from Bugzilla

### Bugs
        
The documents in this index are about the bugs reported in a Bugzilla instance (one
document per bug). BAP can extract information about the reporters, assignees, and
resolvers of these issues. It can also analyze the status, the number of changes, the
number of comments, and other metadata associated with each bug, such as the Product and
Component on which the bug was reported to.

## Data Model

The information for this data set is provided through indices in OpenSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them, it is available below.

| Index Pattern                            | Content                                              |
|------------------------------------------|------------------------------------------------------|
| [bugzilla](../ref/datamodel/bugzilla.md) | Bugs of the Bugzilla instance. One document per bug. |
