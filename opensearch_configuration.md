# OpenSearch configuration


## Custom indices

Indices following these naming patterns are tenant-specific custom indices:
- `custom_<tenant>_*`
- `c_<tenant>_*`

**Visibility**: These indices are accessible to users with the following backend roles:
- `<tenant>_user`: Read access
- `<tenant>_privileged`: Read/write access

Otherwise, they will only be visible to admin users.
