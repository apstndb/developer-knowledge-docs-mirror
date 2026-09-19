---
name: documents/developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks
uri: https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks
title: 'Method: documents.searchDocumentChunks'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

  - [HTTP request](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.HTTP_TEMPLATE)
  - [Query parameters](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.QUERY_PARAMETERS)
  - [Request body](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.request_body)
  - [Response body](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.response_body)
      - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.SearchDocumentChunksResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.aspect)
  - [Try it\!](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#try-it)

Searches for developer knowledge across Google's developer documentation. Returns `  DocumentChunk  ` s based on the user's query. There may be many chunks from the same `  Document  ` . To retrieve full documents, use `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` with the `  DocumentChunk.parent  ` returned in the `  SearchDocumentChunksResponse.results  ` .

### HTTP request

`GET https://developerknowledge.googleapis.com/v1/documents:searchDocumentChunks`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Query parameters

Parameters

`query`

`string`

Required. Provides the raw query string provided by the user, such as "How to create a Cloud Storage bucket?". The query must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

`pageSize`

`integer`

Optional. Specifies the maximum number of results to return. The service may return fewer than this value.

If unspecified, at most 5 results will be returned.

The maximum value is 100; values above 100 will be coerced to 100.

`pageToken`

`string`

Optional. Contains a page token, received from a previous `documents.searchDocumentChunks` call. Provide this to retrieve the subsequent page.

`filter`

`string`

Optional. Applies a strict filter to the search results. The expression supports a subset of the syntax described at <https://google.aip.dev/160> .

While `documents.searchDocumentChunks` returns `  DocumentChunk  ` s, the filter is applied to `DocumentChunk.document` fields.

Supported fields for filtering:

  - `contentLengthBytes` (INTEGER): The length of the `Document.content` field in bytes.
  - `dataSource` (STRING): The source of the document, e.g. `docs.cloud.google.com` . See <https://developers.google.com/knowledge/reference/corpus-reference> for the complete list of data sources in the corpus.
  - `updateTime` (TIMESTAMP): The timestamp of when the document was last meaningfully updated. A meaningful update is one that changes document's markdown content or metadata.
  - `uri` (STRING): The document URI, e.g. `https://docs.cloud.google.com/bigquery/docs/tables` .

INTEGER fields support `=` , `<` , `<=` , `>` , and `>=` operators.

STRING fields support `=` (equals) and `!=` (not equals) operators for **exact match** on the whole string. Partial match, prefix match, and regexp match are not supported.

TIMESTAMP fields support `=` , `<` , `<=` , `>` , and `>=` operators. Timestamps must be in RFC-3339 format, e.g., `"2025-01-01T00:00:00Z"` .

Note: Field names must be in `snake_case` (e.g., `dataSource` ). Values on the right-hand side of filtering expressions must be string literals enclosed in double quotes (e.g., `"docs.cloud.google.com"` ).

You can combine expressions using `AND` , `OR` , and `NOT` (or `-` ) logical operators. `OR` has higher precedence than `AND` . Use parentheses for explicit precedence grouping.

Examples:

  - Filter by `Document.content_length_bytes` : `contentLengthBytes < 50000`
  - `dataSource = "docs.cloud.google.com" OR dataSource = "firebase.google.com"`
  - `dataSource != "firebase.google.com"`
  - `updateTime < "2024-01-01T00:00:00Z"`
  - `updateTime >= "2025-01-22T00:00:00Z" AND (dataSource = "developer.chrome.com" OR dataSource = "web.dev")`
  - `uri = "https://docs.cloud.google.com/release-notes"`

The `filter` string must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

### Request body

The request body must be empty.

### Response body

Response message for `  DeveloperKnowledge.SearchDocumentChunks  ` .

If successful, the response body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (DocumentChunk)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`results[]`

` object ( DocumentChunk  ` )

Contains the search results for the given query. Each `  DocumentChunk  ` in this list contains a snippet of content relevant to the search query. Use the `  DocumentChunk.parent  ` field of each result with `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` to retrieve the full document content.

`nextPageToken`

`string`

Provides a token that can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/devprofiles.full_control`
  - `https://www.googleapis.com/auth/developerprofiles.readonly`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .
