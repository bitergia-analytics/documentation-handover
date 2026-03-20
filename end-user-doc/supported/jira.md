# Jira

Jira is a proprietary issue tracking product developed by Atlassian that allows
bug tracking and agile project management.


## Data from Jira

### Issues and Comments

BAP tracks the collaboration and coordination happening on Jira Issues.

BAP can analyze the data of the contributors who opened the issue and who
reported it. You can track the data of who was assigned to it and who commented
on the issues. Bitergia also calculates time estimation of the issue, time taken
for the issue to be closed, time since there was a last update on the issue,
etc. BAP also analyzes the comments of the issues.


## Data Model

The information for this data set is provided through indices in ElasticSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them it is available below.

| Index Pattern | Content |
| --- | --- |
| [jira](../ref/datamodel/jira.md) | Issues of the Jira tracker |
