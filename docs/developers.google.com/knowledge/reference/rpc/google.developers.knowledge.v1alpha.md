---
name: documents/developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha
uri: https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha
title: Package google.developers.knowledge.v1alpha
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Index

- [`DeveloperKnowledge`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge) (interface)
- [`Answer`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer) (message)
- [`Answer.AnswerCitation`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.AnswerCitation) (message)
- [`Answer.AnswerReference`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.AnswerReference) (message)
- [`Answer.CitationSource`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.CitationSource) (message)
- [`Answer.DocumentReference`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.DocumentReference) (message)
- [`AnswerQueryRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.AnswerQueryRequest) (message)
- [`AnswerQueryResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.AnswerQueryResponse) (message)
- [`BatchGetDocumentsRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.BatchGetDocumentsRequest) (message)
- [`BatchGetDocumentsResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.BatchGetDocumentsResponse) (message)
- [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) (message)
- [`DocumentChunk`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk) (message)
- [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) (enum)
- [`GetDocumentRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.GetDocumentRequest) (message)
- [`SearchDocumentChunksRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.SearchDocumentChunksRequest) (message)
- [`SearchDocumentChunksResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.SearchDocumentChunksResponse) (message)

## DeveloperKnowledge

The Developer Knowledge API provides programmatic access to Google's public developer documentation, enabling you to integrate this knowledge base into your own applications and workflows.

The API is designed to be the canonical source for machine-readable access to Google's developer documentation.

A typical use case is to first use [`DeveloperKnowledge.SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.SearchDocumentChunks) to find relevant page URIs based on a query, and then use [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) to fetch the full content of the top results.

All document content is provided in Markdown format.

**AnswerQuery**

`rpc AnswerQuery( `[`AnswerQueryRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.AnswerQueryRequest)` ) returns ( `[`AnswerQueryResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.AnswerQueryResponse)` )`

Answers a query using grounded generation.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

**BatchGetDocuments**

`rpc BatchGetDocuments( `[`BatchGetDocumentsRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.BatchGetDocumentsRequest)` ) returns ( `[`BatchGetDocumentsResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.BatchGetDocumentsResponse)` )`

Retrieves multiple documents, each with its full Markdown content.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

**GetDocument**

`rpc GetDocument( `[`GetDocumentRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.GetDocumentRequest)` ) returns ( `[`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document)` )`

Retrieves a single document with its full Markdown content.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

**SearchDocumentChunks**

`rpc SearchDocumentChunks( `[`SearchDocumentChunksRequest`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.SearchDocumentChunksRequest)` ) returns ( `[`SearchDocumentChunksResponse`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.SearchDocumentChunksResponse)` )`

Searches for developer knowledge across Google's developer documentation. Returns [`DocumentChunk`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk) s based on the user's query. There may be many chunks from the same [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) . To retrieve full documents, use [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) with the [`DocumentChunk.parent`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk.FIELDS.string.google.developers.knowledge.v1alpha.DocumentChunk.parent) returned in the [`SearchDocumentChunksResponse.results`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.SearchDocumentChunksResponse.FIELDS.repeated.google.developers.knowledge.v1alpha.DocumentChunk.google.developers.knowledge.v1alpha.SearchDocumentChunksResponse.results) .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

## Answer

An answer to a query.

| Fields         |                                                                                                                                                                                                                            |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `answer_text`  | `string` Contains the text of the answer.                                                                                                                                                                                  |
| `citations[]`  | [`AnswerCitation`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.AnswerCitation) Output only. Contains citations for the answer.    |
| `references[]` | [`AnswerReference`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.AnswerReference) Output only. Contains references for the answer. |

## AnswerCitation

Citation info for a segment.

| Fields        |                                                                                                                                                                                                                                            |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_index` | `int32` Output only. Indicates the start of the segment, measured in bytes (UTF-8 unicode), inclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.           |
| `end_index`   | `int32` Output only. Indicates the end of the segment, measured in bytes (UTF-8 unicode), exclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.             |
| `sources[]`   | [`CitationSource`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.CitationSource) Output only. Contains citation sources for the attributed segment. |

## AnswerReference

Represents a reference to a source.

| Fields                                                                                                     |                                                                                                                                                                                                                    |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `content` . Contains the content of the reference. `content` can be only one of the following: |                                                                                                                                                                                                                    |
| `document_reference`                                                                                       | [`DocumentReference`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.DocumentReference) Output only. The reference document. |

## CitationSource

Citation source.

| Fields            |                                                                                                                                                                                                                                                                     |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reference_index` | `int32` Output only. Contains the index of the [`Answer.AnswerReference`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer.AnswerReference) in the `references` repeated field. |

## DocumentReference

Represents a reference to a document.

| Fields           |                                                                                                                                                                                                                                                                      |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document_chunk` | [`DocumentChunk`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk) Output only. Contains the document chunk. The `document_chunk.id` field is not set and will be empty. |

## AnswerQueryRequest

Request message for [`DeveloperKnowledge.AnswerQuery`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.AnswerQuery) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Required. The query to answer.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. Applies a strict filter to the search results used to ground the answer. The expression supports a subset of the syntax described at <a href="https://google.aip.dev/160">https://google.aip.dev/160</a> .</p>
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

## AnswerQueryResponse

Response message for [`DeveloperKnowledge.AnswerQuery`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.AnswerQuery) .

| Fields   |                                                                                                                                                                           |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `answer` | [`Answer`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Answer) The answer to the query. |

## BatchGetDocumentsRequest

Request message for [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) .

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names[]` | `string` Required. Specifies the names of the documents to retrieve. A maximum of 20 documents can be retrieved in a batch. The documents are returned in the same order as the `names` in the request. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` Each name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.                                                                                                                                                                                     |
| `view`    | [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) Optional. Specifies the [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) of the document. If unspecified, [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) defaults to `DOCUMENT_VIEW_CONTENT` . |

## BatchGetDocumentsResponse

Response message for [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) .

| Fields        |                                                                                                                                                                                        |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]` | [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) Contains the documents requested. |

## Document

A Document represents a page of documentation in the Developer Knowledge corpus, like the page at <https://docs.cloud.google.com/storage/docs/creating-buckets> .

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Identifier. Contains the resource name of the document. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`                                                                                                                                                                                    |
| `uri`                  | `string` Output only. Provides the URI of the content, such as `docs.cloud.google.com/storage/docs/creating-buckets` .                                                                                                                                                                                                                                                |
| `content`              | `string` Output only. Contains the full content of the document in Markdown format.                                                                                                                                                                                                                                                                                   |
| `description`          | `string` Output only. Provides a description of the document.                                                                                                                                                                                                                                                                                                         |
| `data_source`          | `string` Output only. Specifies the data source of the document. Example data source: `firebase.google.com`                                                                                                                                                                                                                                                           |
| `title`                | `string` Output only. Provides the title of the document.                                                                                                                                                                                                                                                                                                             |
| `update_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Represents the timestamp when the content or metadata of the document was last updated.                                                                                                                                                                                |
| `view`                 | [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) Output only. Specifies the [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) of the document. |
| `content_length_bytes` | `int32` Output only. The length of the `content` field in bytes.                                                                                                                                                                                                                                                                                                      |

## DocumentChunk

A DocumentChunk represents a piece of content from a [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) in the DeveloperKnowledge corpus. To fetch the entire document content, pass the `parent` to [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`          | `string` Output only. Contains the resource name of the document this chunk is from. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `id`              | `string` Output only. Specifies the ID of this chunk within the document. The chunk ID is unique within a document, but not globally unique across documents. The chunk ID is not stable and may change over time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `content`         | `string` Output only. Contains the content of the document chunk.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `document`        | [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) Output only. Represents metadata about the [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) this chunk is from. The [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) of this [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) message will be set to `DOCUMENT_VIEW_BASIC` . It is included here for convenience so that clients do not need to call [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) if they only need the metadata fields. Otherwise, clients should use [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) to fetch the full document content. |
| `relevance_score` | `double` Output only. Represents the relevance score of the chunk to the search query. Higher score indicates higher chunk relevance. The score is in range \[0.0, 1.0\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## DocumentView

Specifies which fields of the [`Document`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document) are included.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>DOCUMENT_VIEW_UNSPECIFIED</code></td>
<td>The default / unset value. See each API method for its default value if <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView"><code>DocumentView</code></a> is not specified.</td>
</tr>
<tr class="even">
<td><code>DOCUMENT_VIEW_BASIC</code></td>
<td><p>Includes only the basic metadata fields:</p>
<ul>
<li><code>name</code></li>
<li><code>uri</code></li>
<li><code>data_source</code></li>
<li><code>title</code></li>
<li><code>description</code></li>
<li><code>update_time</code></li>
<li><code>view</code></li>
<li><code>content_length_bytes</code></li>
</ul>
<p>This is the default of view for <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.SearchDocumentChunks"><code>DeveloperKnowledge.SearchDocumentChunks</code></a> .</p></td>
</tr>
<tr class="odd">
<td><code>DOCUMENT_VIEW_FULL</code></td>
<td>Includes all <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.Document"><code>Document</code></a> fields.</td>
</tr>
<tr class="even">
<td><code>DOCUMENT_VIEW_CONTENT</code></td>
<td><p>Includes the <code>DOCUMENT_VIEW_BASIC</code> fields and the <code>content</code> field.</p>
<p>This is the default of view for <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument"><code>DeveloperKnowledge.GetDocument</code></a> and <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments"><code>DeveloperKnowledge.BatchGetDocuments</code></a> .</p></td>
</tr>
</tbody>
</table>

## GetDocumentRequest

Request message for [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) .

| Fields |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. Specifies the name of the document to retrieve. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` The name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.                                                                                                                                                                                                                                                                                                               |
| `view` | [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) Optional. Specifies the [`DocumentView`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentView) of the document. If unspecified, [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) defaults to `DOCUMENT_VIEW_CONTENT` . |

## SearchDocumentChunksRequest

Request message for [`DeveloperKnowledge.SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.SearchDocumentChunks) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
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
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Optional. Specifies the maximum number of results to return. The service may return fewer than this value.</p>
<p>If unspecified, at most 5 results will be returned.</p>
<p>The maximum value is 100; values above 100 will be coerced to 100.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Optional. Contains a page token, received from a previous <code>SearchDocumentChunks</code> call. Provide this to retrieve the subsequent page.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. Applies a strict filter to the search results. The expression supports a subset of the syntax described at <a href="https://google.aip.dev/160">https://google.aip.dev/160</a> .</p>
<p>While <code>SearchDocumentChunks</code> returns <a href="https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk"><code>DocumentChunk</code></a> s, the filter is applied to <code>DocumentChunk.document</code> fields.</p>
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

## SearchDocumentChunksResponse

Response message for [`DeveloperKnowledge.SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.SearchDocumentChunks) .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`       | [`DocumentChunk`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk) Contains the search results for the given query. Each [`DocumentChunk`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk) in this list contains a snippet of content relevant to the search query. Use the [`DocumentChunk.parent`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DocumentChunk.FIELDS.string.google.developers.knowledge.v1alpha.DocumentChunk.parent) field of each result with [`DeveloperKnowledge.GetDocument`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.GetDocument) or [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rpc/google.developers.knowledge.v1alpha#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) to retrieve the full document content. |
| `next_page_token` | `string` Provides a token that can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
