# All Enriched

This index doesn't hold data from a particular data source. Instead, it's a dynamic
merge of *all kinds of contributions* being tracked.

It is _dynamic_ because the data is physically stored in the original indexes and
is merged on the fly for each query.

It merges all kinds of contributions being tracked in the particular instance. Since the
list of data sources tracked is configurable, your list of fields will differ from those
of other customers.

Since each type of contribution has a different set of fields, the fields served by
this index are not uniform for each element retrieved. You get a different set of fields
depending on the data source each element comes from. Please refer to the data models of
each data source (git commits, github issues, gitlab merge requests, jira tickets, etc)
for more details.
