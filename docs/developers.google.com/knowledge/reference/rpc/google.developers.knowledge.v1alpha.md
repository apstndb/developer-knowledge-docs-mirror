---
name: documents/developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha
uri: https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha
title: Package google.developers.knowledge.v1alpha
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Index

  - `  DeveloperKnowledge  ` (interface)
  - `  Answer  ` (message)
  - `  Answer.AnswerCitation  ` (message)
  - `  Answer.AnswerReference  ` (message)
  - `  Answer.CitationSource  ` (message)
  - `  Answer.DocumentReference  ` (message)
  - `  AnswerQueryRequest  ` (message)
  - `  AnswerQueryResponse  ` (message)
  - `  BatchGetDocumentsRequest  ` (message)
  - `  BatchGetDocumentsResponse  ` (message)
  - `  Document  ` (message)
  - `  DocumentChunk  ` (message)
  - `  DocumentView  ` (enum)
  - `  GetDocumentRequest  ` (message)
  - `  SearchDocumentChunksRequest  ` (message)
  - `  SearchDocumentChunksResponse  ` (message)

## DeveloperKnowledge

The Developer Knowledge API provides programmatic access to Google's public developer documentation, enabling you to integrate this knowledge base into your own applications and workflows.

The API is designed to be the canonical source for machine-readable access to Google's developer documentation.

A typical use case is to first use `  DeveloperKnowledge.SearchDocumentChunks  ` to find relevant page URIs based on a query, and then use `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` to fetch the full content of the top results.

All document content is provided in Markdown format.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>AnswerQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc AnswerQuery(              AnswerQueryRequest            </code> ) returns ( <code dir="ltr" translate="no">             AnswerQueryResponse            </code> )</p>
<p>Answers a query using grounded generation.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/devprofiles.full_control</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/developerprofiles.readonly</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://developers.google.com/identity/protocols/OAuth2">OAuth 2.0 Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>BatchGetDocuments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc BatchGetDocuments(              BatchGetDocumentsRequest            </code> ) returns ( <code dir="ltr" translate="no">             BatchGetDocumentsResponse            </code> )</p>
<p>Retrieves multiple documents, each with its full Markdown content.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/devprofiles.full_control</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/developerprofiles.readonly</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://developers.google.com/identity/protocols/OAuth2">OAuth 2.0 Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetDocument</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetDocument(              GetDocumentRequest            </code> ) returns ( <code dir="ltr" translate="no">             Document            </code> )</p>
<p>Retrieves a single document with its full Markdown content.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/devprofiles.full_control</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/developerprofiles.readonly</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://developers.google.com/identity/protocols/OAuth2">OAuth 2.0 Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SearchDocumentChunks</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc SearchDocumentChunks(              SearchDocumentChunksRequest            </code> ) returns ( <code dir="ltr" translate="no">             SearchDocumentChunksResponse            </code> )</p>
<p>Searches for developer knowledge across Google's developer documentation. Returns <code dir="ltr" translate="no">            DocumentChunk           </code> s based on the user's query. There may be many chunks from the same <code dir="ltr" translate="no">            Document           </code> . To retrieve full documents, use <code dir="ltr" translate="no">            DeveloperKnowledge.GetDocument           </code> or <code dir="ltr" translate="no">            DeveloperKnowledge.BatchGetDocuments           </code> with the <code dir="ltr" translate="no">            DocumentChunk.parent           </code> returned in the <code dir="ltr" translate="no">            SearchDocumentChunksResponse.results           </code> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/devprofiles.full_control</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/developerprofiles.readonly</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://developers.google.com/identity/protocols/OAuth2">OAuth 2.0 Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## Answer

An answer to a query.

Fields

`answer_text`

`string`

Contains the text of the answer.

`citations[]`

`  AnswerCitation  `

Output only. Contains citations for the answer.

`references[]`

`  AnswerReference  `

Output only. Contains references for the answer.

## AnswerCitation

Citation info for a segment.

Fields

`start_index`

`int32`

Output only. Indicates the start of the segment, measured in bytes (UTF-8 unicode), inclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.

`end_index`

`int32`

Output only. Indicates the end of the segment, measured in bytes (UTF-8 unicode), exclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.

`sources[]`

`  CitationSource  `

Output only. Contains citation sources for the attributed segment.

## AnswerReference

Represents a reference to a source.

Fields

Union field `content` . Contains the content of the reference. `content` can be only one of the following:

`document_reference`

`  DocumentReference  `

Output only. The reference document.

## CitationSource

Citation source.

Fields

`reference_index`

`int32`

Output only. Contains the index of the `  Answer.AnswerReference  ` in the `references` repeated field.

## DocumentReference

Represents a reference to a document.

Fields

`document_chunk`

`  DocumentChunk  `

Output only. Contains the document chunk. The `document_chunk.id` field is not set and will be empty.

## AnswerQueryRequest

Request message for `  DeveloperKnowledge.AnswerQuery  ` .

Fields

`query`

`string`

Required. The query to answer.

`filter`

`string`

Optional. Applies a strict filter to the search results used to ground the answer. The expression supports a subset of the syntax described at <https://google.aip.dev/160> .

Supported fields for filtering:

  - `content_length_bytes` (INTEGER): The length of the `Document.content` field in bytes.
  - `data_source` (STRING): The source of the document, e.g. `docs.cloud.google.com` . See <https://developers.google.com/knowledge/reference/corpus-reference> for the complete list of data sources in the corpus.
  - `update_time` (TIMESTAMP): The timestamp of when the document was last meaningfully updated. A meaningful update is one that changes document's markdown content or metadata.
  - `uri` (STRING): The document URI, e.g. `https://docs.cloud.google.com/bigquery/docs/tables` .

INTEGER fields support `=` , `<` , `<=` , `>` , and `>=` operators.

STRING fields support `=` (equals) and `!=` (not equals) operators for **exact match** on the whole string. Partial match, prefix match, and regexp match are not supported.

TIMESTAMP fields support `=` , `<` , `<=` , `>` , and `>=` operators. Timestamps must be in RFC-3339 format, e.g., `"2025-01-01T00:00:00Z"` .

You can combine expressions using `AND` , `OR` , and `NOT` (or `-` ) logical operators. `OR` has higher precedence than `AND` . Use parentheses for explicit precedence grouping.

Examples:

  - Filter by `Document.content_length_bytes` : `content_length_bytes < 50000`
  - `data_source = "docs.cloud.google.com" OR data_source = "firebase.google.com"`
  - `data_source != "firebase.google.com"`
  - `update_time < "2024-01-01T00:00:00Z"`
  - `update_time >= "2025-01-22T00:00:00Z" AND (data_source = "developer.chrome.com" OR data_source = "web.dev")`
  - `uri = "https://docs.cloud.google.com/release-notes"`

The `filter` string must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

## AnswerQueryResponse

Response message for `  DeveloperKnowledge.AnswerQuery  ` .

Fields

`answer`

`  Answer  `

The answer to the query.

## BatchGetDocumentsRequest

Request message for `  DeveloperKnowledge.BatchGetDocuments  ` .

Fields

`names[]`

`string`

Required. Specifies the names of the documents to retrieve. A maximum of 20 documents can be retrieved in a batch. The documents are returned in the same order as the `names` in the request.

Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

Each name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

`view`

`  DocumentView  `

Optional. Specifies the `  DocumentView  ` of the document. If unspecified, `  DeveloperKnowledge.BatchGetDocuments  ` defaults to `DOCUMENT_VIEW_CONTENT` .

## BatchGetDocumentsResponse

Response message for `  DeveloperKnowledge.BatchGetDocuments  ` .

Fields

`documents[]`

`  Document  `

Contains the documents requested.

## Document

A Document represents a page of documentation in the Developer Knowledge corpus, like the page at <https://docs.cloud.google.com/storage/docs/creating-buckets> .

Fields

`name`

`string`

Identifier. Contains the resource name of the document. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

`uri`

`string`

Output only. Provides the URI of the content, such as `docs.cloud.google.com/storage/docs/creating-buckets` .

`content`

`string`

Output only. Contains the full content of the document in Markdown format.

`description`

`string`

Output only. Provides a description of the document.

`data_source`

`string`

Output only. Specifies the data source of the document. Example data source: `firebase.google.com`

`title`

`string`

Output only. Provides the title of the document.

`update_time`

`  Timestamp  `

Output only. Represents the timestamp when the content or metadata of the document was last updated.

`view`

`  DocumentView  `

Output only. Specifies the `  DocumentView  ` of the document.

`content_length_bytes`

`int32`

Output only. The length of the `content` field in bytes.

## DocumentChunk

A DocumentChunk represents a piece of content from a `  Document  ` in the DeveloperKnowledge corpus. To fetch the entire document content, pass the `parent` to `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` .

Fields

`parent`

`string`

Output only. Contains the resource name of the document this chunk is from. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

`id`

`string`

Output only. Specifies the ID of this chunk within the document. The chunk ID is unique within a document, but not globally unique across documents. The chunk ID is not stable and may change over time.

`content`

`string`

Output only. Contains the content of the document chunk.

`document`

`  Document  `

Output only. Represents metadata about the `  Document  ` this chunk is from. The `  DocumentView  ` of this `  Document  ` message will be set to `DOCUMENT_VIEW_BASIC` . It is included here for convenience so that clients do not need to call `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` if they only need the metadata fields. Otherwise, clients should use `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` to fetch the full document content.

`relevance_score`

`double`

Output only. Represents the relevance score of the chunk to the search query. Higher score indicates higher chunk relevance. The score is in range \[0.0, 1.0\].

## DocumentView

Specifies which fields of the `  Document  ` are included.

Enums

`DOCUMENT_VIEW_UNSPECIFIED`

The default / unset value. See each API method for its default value if `  DocumentView  ` is not specified.

`DOCUMENT_VIEW_BASIC`

Includes only the basic metadata fields:

  - `name`
  - `uri`
  - `data_source`
  - `title`
  - `description`
  - `update_time`
  - `view`
  - `content_length_bytes`

This is the default of view for `  DeveloperKnowledge.SearchDocumentChunks  ` .

`DOCUMENT_VIEW_FULL`

Includes all `  Document  ` fields.

`DOCUMENT_VIEW_CONTENT`

Includes the `DOCUMENT_VIEW_BASIC` fields and the `content` field.

This is the default of view for `  DeveloperKnowledge.GetDocument  ` and `  DeveloperKnowledge.BatchGetDocuments  ` .

## GetDocumentRequest

Request message for `  DeveloperKnowledge.GetDocument  ` .

Fields

`name`

`string`

Required. Specifies the name of the document to retrieve. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

The name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

`view`

`  DocumentView  `

Optional. Specifies the `  DocumentView  ` of the document. If unspecified, `  DeveloperKnowledge.GetDocument  ` defaults to `DOCUMENT_VIEW_CONTENT` .

## SearchDocumentChunksRequest

Request message for `  DeveloperKnowledge.SearchDocumentChunks  ` .

Fields

`query`

`string`

Required. Provides the raw query string provided by the user, such as "How to create a Cloud Storage bucket?". The query must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

`page_size`

`int32`

Optional. Specifies the maximum number of results to return. The service may return fewer than this value.

If unspecified, at most 5 results will be returned.

The maximum value is 100; values above 100 will be coerced to 100.

`page_token`

`string`

Optional. Contains a page token, received from a previous `SearchDocumentChunks` call. Provide this to retrieve the subsequent page.

`filter`

`string`

Optional. Applies a strict filter to the search results. The expression supports a subset of the syntax described at <https://google.aip.dev/160> .

While `SearchDocumentChunks` returns `  DocumentChunk  ` s, the filter is applied to `DocumentChunk.document` fields.

Supported fields for filtering:

  - `content_length_bytes` (INTEGER): The length of the `Document.content` field in bytes.
  - `data_source` (STRING): The source of the document, e.g. `docs.cloud.google.com` . See <https://developers.google.com/knowledge/reference/corpus-reference> for the complete list of data sources in the corpus.
  - `update_time` (TIMESTAMP): The timestamp of when the document was last meaningfully updated. A meaningful update is one that changes document's markdown content or metadata.
  - `uri` (STRING): The document URI, e.g. `https://docs.cloud.google.com/bigquery/docs/tables` .

INTEGER fields support `=` , `<` , `<=` , `>` , and `>=` operators.

STRING fields support `=` (equals) and `!=` (not equals) operators for **exact match** on the whole string. Partial match, prefix match, and regexp match are not supported.

TIMESTAMP fields support `=` , `<` , `<=` , `>` , and `>=` operators. Timestamps must be in RFC-3339 format, e.g., `"2025-01-01T00:00:00Z"` .

Note: Field names must be in `snake_case` (e.g., `data_source` ). Values on the right-hand side of filtering expressions must be string literals enclosed in double quotes (e.g., `"docs.cloud.google.com"` ).

You can combine expressions using `AND` , `OR` , and `NOT` (or `-` ) logical operators. `OR` has higher precedence than `AND` . Use parentheses for explicit precedence grouping.

Examples:

  - Filter by `Document.content_length_bytes` : `content_length_bytes < 50000`
  - `data_source = "docs.cloud.google.com" OR data_source = "firebase.google.com"`
  - `data_source != "firebase.google.com"`
  - `update_time < "2024-01-01T00:00:00Z"`
  - `update_time >= "2025-01-22T00:00:00Z" AND (data_source = "developer.chrome.com" OR data_source = "web.dev")`
  - `uri = "https://docs.cloud.google.com/release-notes"`

The `filter` string must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

## SearchDocumentChunksResponse

Response message for `  DeveloperKnowledge.SearchDocumentChunks  ` .

Fields

`results[]`

`  DocumentChunk  `

Contains the search results for the given query. Each `  DocumentChunk  ` in this list contains a snippet of content relevant to the search query. Use the `  DocumentChunk.parent  ` field of each result with `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` to retrieve the full document content.

`next_page_token`

`string`

Provides a token that can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.
