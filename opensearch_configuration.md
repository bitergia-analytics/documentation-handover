# OpenSearch configuration

OpenSearch is configured with role-based access control to manage data visibility
and user permissions. This document outlines key configuration aspects including
pseudonymization and custom indices.

- [Pseudoanonymization](#pseudoanonymization)
- [Custom indices](#custom-indices)

## Pseudoanonymization

To pseudonymize personal data fields (committer, owner, name, login, etc.),
users or backend roles need to be assigned the following role:

- `bap_<tenant>_pseudonymize_role`

This role grants access to view data with personal identifiers masked,
protecting individual privacy while maintaining analytical capabilities.

If you want to pseudonymize more fields, edit the role in OpenSearch Dashboards
under **Security → Roles → `bap_<tenant>_pseudonymize_role`** and modify the
field masking configuration in **Index permissions → Anonymization** to include
additional fields that should be protected.

### Example

A data analyst with the `bap_<tenant>_pseudonymize_role` would see commit data like this:

**Original data** (without pseudonymization role):

```json
{
    "commit_id": "a1b2c3d4",
    "author_name": "John Smith",
    "author_username": "j_smith",
    ...
}
```

**Pseudonymized data** (with pseudonymization role):

```json
{
    "commit_id": "a1b2c3d4",
    "author_name": "<masked>",
    "author_username": "<masked>",
    ...
}
```

This allows the analyst to perform statistical analysis on commit patterns and metrics
without exposing individual contributor identities.


## Custom indices

Custom indices allow you to store and analyze data that is specific to your
organization's needs, beyond the standard data collected by Bitergia Analytics.
For example, you might want to:

- Integrate data from internal tools or systems
- Create derived metrics combining multiple data sources
- Store preprocessed or aggregated data for faster queries
- Maintain custom reports or dashboards with specialized data structures

Indices following these naming patterns are tenant-specific custom indices:

- `custom_<tenant>_*`
- `c_<tenant>_*`

**Visibility**: These indices are accessible to users with the following backend roles:

- `<tenant>_user`: Read access
- `<tenant>_privileged`: Read/write access

### Example

A company tracking both GitHub activity and internal code review metrics might create
a custom index to correlate this data:

**Index name**: `custom_<tenant>_code_reviews`

**Sample document**:

```json
{
    "review_id": "CR-12345",
    "github_pr": "https://github.com/xxx/yyy/pull/456",
    "reviewer": "jane.doe",
    "review_date": "2024-01-15",
    "internal_score": 8.5,
    "time_to_review_hours": 4.2
}
```

This custom index would be accessible to users with `<tenant>_user` (read) or
`<tenant>_privileged` (read/write) roles, allowing the team to build dashboards
combining GitHub PR data with internal review metrics.
