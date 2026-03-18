# FAQ

## Identities

<details>
<summary><strong>How to add a new organization?</strong></summary>

You can add a new organization via SortingHat.

See more information [here](../advanced/affiliations.md#adding-a-new-organization)
</details>

<details>
<summary><strong>How to remove an organization?</strong></summary>

You can remove an organization via SortingHat.

See more information [here](../advanced/affiliations.md#removing-an-organization)
</details>

<details>
<summary><strong>How to assign an e-mail domain to an organization?</strong></summary>

You can assign an e-mail domain to an organization via SortingHat.

See more information [here](../advanced/affiliations.md#adding-an-e-mail-domain-to-an-organization)
</details>

<details>
<summary><strong>How to enroll a person to an organization during a time interval?</strong></summary>

You can enroll profiles via SortingHat.

See more information [here](../advanced/affiliations.md#enrolling-a-person-to-an-organization)
</details>

<details>
<summary><strong>How to prevent that affiliations removed from a contributor are restored?</strong></summary>

You can do it via SortingHat.

See more information [here](../advanced/affiliations.md#preventing-that-affiliations-removed-from-a-contributor-are-restored)
</details>

<details>
<summary><strong>How to un-enroll a person from an organization?</strong></summary>

You can un-enroll a person via SortingHat.

See more information [here](../advanced/affiliations.md#un-enrolling-a-person-from-an-organization)
</details>

<details>
<summary><strong>How to correctly enroll a person to different organizations during consecutive time periods avoiding overlapping dates?</strong></summary>

You need to understand how dates work.

See more information [here](../advanced/affiliations.md#contributor-activity-is-labeled-with-a-single-company-when-shehe-is-enrolled-with-more-companies)
</details>

<details>
<summary><strong>How to enroll a person to two organizations during the same time intervals?</strong></summary>

Intervals should not overlap.

See more information [here](../advanced/affiliations.md#contributor-activity-is-labeled-with-a-single-company-when-shehe-is-enrolled-with-more-companies)
</details>

<details>
<summary><strong>How to mark an identity as a bot?</strong></summary>

You can mark identities as bots via SortingHat.

See more information [here](../advanced/affiliations.md#marking-bots)
</details>

<details>
<summary><strong>How many types of matching do exist?</strong></summary>

There are 4.

See more information [here](../advanced/affiliations.md#types-of-matching)
</details>

<details>
<summary><strong>How long does it take to see the changes in SortingHat reflected in the dashboard?</strong></summary>

The time depends on the amount of data available in the data source

See more information [here](../advanced/affiliations.md#changes-are-not-visible-in-the-metrics-dashboard)
</details>

<details>
<summary><strong>What is the organization JSON file?</strong></summary>

The organization JSON file contains a list of organizations and their domains.

See more information [here](../advanced/projects_json_file.md)
</details>


## Data sources management

<details>
<summary><strong>How to add a new repository?</strong></summary>

You have to edit `projects.json` file.

See more information [here](../advanced/projects_json_file.md)
</details>

<details>
<summary><strong>How to add labels to repositories?</strong></summary>

You have to edit `projects.json` file.

See more information [here](../advanced/projects_json_file.md)
</details>

<details>
<summary><strong>How to track private repositories on GitHub?</strong></summary>

We need permission.

See more information [here](../supported/github.md#tracking-private-repositories)
</details>

<details>
<summary><strong>How to track private repositories on GitLab?</strong></summary>

We need permission.

See more information [here](../supported/gitlab.md#tracking-private-repositories)
</details>


## Dashboards

<details>
<summary><strong>How to inspect an index from the web user interface?</strong></summary>

On `Discover` section.

See more information [here](../advanced/explore.md#inspecting-an-index-from-the-web-user-interface)
</details>

<details>
<summary><strong>How to share a dashboard?</strong></summary>

You have to be logged in and click on `Share`.

See more information [here](../new/reporting_and_sharing.md#sharing-a-dashboard)
</details>

<details>
<summary><strong>How to properly save a new visualization or dashboard?</strong></summary>

You have to mark `Save as new visualization`.

See more information [here](../new/custom_visualizations.md#saving-new-visualizations)
</details>

<details>
<summary><strong>How to edit a visualization?</strong></summary>

You have to click on `Edit`, then the `gear` and then `Edit visualization`.

See more information [here](../new/custom_visualizations.md#editing-visualizations)
</details>

<details>
<summary><strong>How to edit the name of a visualization?</strong></summary>

You have to edit the visualization.

See more information [here](../new/custom_visualizations.md#renaming-visualizations)
</details>

<details>
<summary><strong>How to create a visualization?</strong></summary>

You have to click on `Edit` and then on `Create new`.

See more information [here](../new/custom_visualizations.md#creating-visualizations)
</details>

<details>
<summary><strong>How to edit a dashboard?</strong></summary>

You have to click on `Edit` to enter in edition mode.

See more information [here](../new/custom_visualizations.md#editing-a-dashboard)
</details>

<details>
<summary><strong>How to create a dashboard?</strong></summary>

You have to go to `Dashboard` section and perform editions on edition mode.

See more information [here](../new/custom_visualizations.md#creating-dashboards)
</details>

<details>
<summary><strong>How to edit the quick ranges offered by the time filter?</strong></summary>

You have to go to the left of the dashboards bar, next to the wise owl icon and
open the dropdown menu. Then, find the `Dashboards Management` section and select
the `Advanced Settings` option. Then, go to the `Time filter quick ranges` section
and edit them as needed. Remember to re-load the page after saving your changes.
</details>

## Metrics

<details>
<summary><strong>Why are results sometimes inaccurate?</strong></summary>

OpenSearch Dashboards' counts are approximated. It uses a **cardinality aggregations**
algorithm to count data, which prioritize performace over accuracy. These cardinality
algorithms are designed to handle big ammounts of data, offering results fast. For 
this reason, there's always an error associated to these counts. Usually, you will 
find these problems with **unique counts** (e.g. total count of commits).

You can learn more about this topic and the precision error in the 
[cardinality aggregation section](https://opensearch.org/docs/latest/opensearch/metric-agg/#cardinality) 
of the OpenSearch Dashboards' documentation.
</details>

## User Management

<details>
<summary><strong>How to change my password?</strong></summary>

When you are logged in, at the right end of the dashboard toolbar, next to the
OpenSearch help icon, there's a letter in a circle signalling your user management
options. Click on it and a menu will drop down.

The `Reset password` option lets you modify your password, provided you
know your current one.

SortingHat provides a similar procedure. For simplicity, we tend to provide the same
credentials for both tools. Consider changing both to keep having only one password.
</details>
