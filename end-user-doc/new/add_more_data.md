# Add More Data

The data you can add to your instance can be basically classified in two buckets:

  - data repositories: source code repositories, trackers, mailing lists, chat rooms, etc.
  - affiliations: contributor data (name, email, usernames), organizations (names and
    domains) and the relationship between contributors and organizations (enrollments).

## How to Add More Data
In case you want to add more repositories to your Bitergia Analytics instance, you can do so by modifying the [projects configuration file](../advanced/projects_json_file.md). This JSON file contains the list of repositories for each project.

## Organizing Data

Some customers organize their repositories in groups. This is especially useful when you
have many.

### By Project - standard

An open source project may have more than one repository, so it usually makes sense to look
at them together as a whole. This is the standard way of organizing repositories.

The project-repository assignment is custom to your dashboard and you can customize it
using the [projects.json file](../advanced/projects_json_file.md). Once assigned, the data
of each repository gets a `project` field with the assigned value that can then be used to filter.

### Classifying Projects - advanced

Some open source communities have several open source projects that fall into different
groupings. For example,

- per maturity level of the project governance: Sandbox, Incubating, Graduated.
- per technology: IoT, AI, Web, Network, Multimedia, Critical, ...
- per vertical market segment: Aerospatial, Medical, E-commerce, Automotive, ...
 
You can create custom fields per project in the [projects.json file](../advanced/projects_json_file.md)
to create other independent classifications to support these groupings. You can customize
this behavior under the project using the `meta` field to add extra fields or using the
`labels` for each repository. Check all the options at the [GrimoireLab SirMordred documentation](https://github.com/chaoss/grimoirelab-sirmordred?tab=readme-ov-file#projectsjson-).

### Classifying Repositories - advanced

It can be useful to create custom groupings of repositories that span multiple projects.
For example, in a community of multiple projects, each project could have a repository
dedicated to receiving improvement requests. Analyzing the activity across all projects
can give insights into who is making improvement requests not just in one project but
across the community.

We create these custom groupings of repositories by assigning custom labels. This allows
for finer granularity but is also very burdensome to maintain as projects evolve and
repositories get added and removed.

## Affiliation Data

The information about how to extend data from contributors or/and organizations is
available in the [affiliations](../advanced/affiliations.md) section.
