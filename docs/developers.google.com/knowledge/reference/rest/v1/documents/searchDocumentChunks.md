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
- [Try it!](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#try-it)

Searches for developer knowledge across Google's developer documentation. Returns [`DocumentChunk`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk) s based on the user's query. There may be many chunks from the same [`Document`](https://developers.google.com/knowledge/reference/rest/v1/documents#Document) . To retrieve full documents, use [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rest/v1/documents/get#google.developers.knowledge.v1.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet#google.developers.knowledge.v1.DeveloperKnowledge.BatchGetDocuments) with the [`DocumentChunk.parent`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk#FIELDS.parent) returned in the [`SearchDocumentChunksResponse.results`](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#body.SearchDocumentChunksResponse.FIELDS.results) .

### HTTP request

`GET https://developerknowledge.googleapis.com/v1/documents:searchDocumentChunks`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Query parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Required. Provides the raw query string provided by the user, such as "How to create a Cloud Storage bucket?". The query must not exceed 500 characters; values longer than 500 characters will result in an <code>INVALID_ARGUMENT</code> error.</p></td>
</tr>
<tr class="even">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>Optional. Specifies the maximum number of results to return. The service may return fewer than this value.</p>
<p>If unspecified, at most 5 results will be returned.</p>
<p>The maximum value is 100; values above 100 will be coerced to 100.</p></td>
</tr>
<tr class="odd">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>Optional. Contains a page token, received from a previous <code>documents.searchDocumentChunks</code> call. Provide this to retrieve the subsequent page.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. Applies a strict filter to the search results. The expression supports a subset of the syntax described at <a href="https://google.aip.dev/160">https://google.aip.dev/160</a> .</p>
<p>While <code>documents.searchDocumentChunks</code> returns <a href="https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk"><code>DocumentChunk</code></a> s, the filter is applied to <code>DocumentChunk.document</code> fields.</p>
<p>Supported fields for filtering:</p>
<ul>
<li><code>content_length_bytes</code> (INTEGER): The length of the <code>Document.content</code> field in bytes.</li>
<li><code>data_source</code> (STRING): The source of the document, e.g. <code>docs.cloud.google.com</code> . See <a href="https://developers.google.com/knowledge/reference/corpus-reference">https://developers.google.com/knowledge/reference/corpus-reference</a> for the complete list of data sources in the corpus.</li>
<li><code>update_time</code> (TIMESTAMP): The timestamp of when the document was last meaningfully updated. A meaningful update is one that changes document's markdown content or metadata.</li>
<li><code>uri</code> (STRING): The document URI, e.g. <code>https://docs.cloud.google.com/bigquery/docs/tables</code> .</li>
</ul>
<p>INTEGER fields support <code>=</code> , <code>&lt;</code> , <code>&lt;=</code> , <code>&gt;</code> , and <code>&gt;=</code> operators.</p>
<p>STRING fields support <code>=</code> (equals) and <code>!=</code> (not equals) operators for <strong>exact match</strong> on the whole string. Partial match, prefix match, and regexp match are not supported.</p>
<p>TIMESTAMP fields support <code>=</code> , <code>&lt;</code> , <code>&lt;=</code> , <code>&gt;</code> , and <code>&gt;=</code> operators. Timestamps must be in RFC-3339 format, e.g., <code>"2025-01-01T00:00:00Z"</code> .</p>
<p>Note: Field names must be in <code>snake_case</code> (e.g., <code>data_source</code> ). Values on the right-hand side of filtering expressions must be string literals enclosed in double quotes (e.g., <code>"docs.cloud.google.com"</code> ).</p>
<p>You can combine expressions using <code>AND</code> , <code>OR</code> , and <code>NOT</code> (or <code>-</code> ) logical operators. <code>OR</code> has higher precedence than <code>AND</code> . Use parentheses for explicit precedence grouping.</p>
<p>Examples:</p>
<ul>
<li>Filter by <code>Document.content_length_bytes</code> : <code>content_length_bytes &lt; 50000</code></li>
<li><code>data_source = "docs.cloud.google.com" OR data_source = "firebase.google.com"</code></li>
<li><code>data_source != "firebase.google.com"</code></li>
<li><code>update_time &lt; "2024-01-01T00:00:00Z"</code></li>
<li><code>update_time &gt;= "2025-01-22T00:00:00Z" AND (data_source = "developer.chrome.com" OR data_source = "web.dev")</code></li>
<li><code>uri = "https://docs.cloud.google.com/release-notes"</code></li>
</ul>
<p>The <code>filter</code> string must not exceed 500 characters; values longer than 500 characters will result in an <code>INVALID_ARGUMENT</code> error.</p></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

Response message for [`DeveloperKnowledge.SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#google.developers.knowledge.v1.DeveloperKnowledge.SearchDocumentChunks) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "results": [
    {
      object (DocumentChunk)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`     | `object ( `[`DocumentChunk`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk)` )` Contains the search results for the given query. Each [`DocumentChunk`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk) in this list contains a snippet of content relevant to the search query. Use the [`DocumentChunk.parent`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk#FIELDS.parent) field of each result with [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rest/v1/documents/get#google.developers.knowledge.v1.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet#google.developers.knowledge.v1.DeveloperKnowledge.BatchGetDocuments) to retrieve the full document content. |
| `nextPageToken` | `string` Provides a token that can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .
