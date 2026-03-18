# OpenSearch API

The data endpoint exposes some OpenSearch web (HTTPS) APIs. It provides a
programming-friendly way to interact with the data.

This section provides the minimal pointers to start using this endpoint.


## Access

The data endpoint might be enabled for your instance or not. It would be reachable as
`https://my_bap_instance.biterg.io/data`.

The available data and operations depend on how the userid used to connect is configured
in the platform. Specifically, on the permissions granted to the profile assigned to the
user account.

The authentication is via `userid` and password, and their transmission is protected by
the HTTPS secure protocol. Make sure you **never** call via the unprotected HTTP
protocol.


## API documentation

The OpenSearch
[REST APIs](https://docs.opensearch.org/docs/latest/api-reference/#rest-apis) are
documented upstream. The most relevant are the
[Document APIs](https://docs.opensearch.org/docs/latest/api-reference/document-apis/index/)
(_document_ is the word in OpenSearch jargon for _data record_). And there are
[OpenSearch API clients](https://docs.opensearch.org/docs/latest/clients/) available for
several programming languages.

## Query langages

The default query language is OpenSearch's standard
[Domain Specific Language (DSL)](https://docs.opensearch.org/docs/latest/query-dsl)
, which you can find in the dashboard filters and when inspecting visualizations.

If enabled, you can also use [SQL](sql.md) with limitations.


## Index structures

Please refer to the section describing the
[supported data sources](../supported/index.md) for details of the data structures and
their fields.

You can also learn about them [exploring the data](explore.md).
