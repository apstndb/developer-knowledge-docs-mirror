---
name: documents/developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery
uri: https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery
title: 'Method: answerQuery'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

- [HTTP request](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.HTTP_TEMPLATE)
- [Request body](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.request_body)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.response_body)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.AnswerQueryResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.aspect)
- [Answer](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#Answer)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#Answer.SCHEMA_REPRESENTATION)
- [AnswerCitation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerCitation)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerCitation.SCHEMA_REPRESENTATION)
- [CitationSource](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#CitationSource)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#CitationSource.SCHEMA_REPRESENTATION)
- [AnswerReference](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerReference)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerReference.SCHEMA_REPRESENTATION)
- [DocumentReference](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#DocumentReference)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#DocumentReference.SCHEMA_REPRESENTATION)
- [Try it!](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#try-it)

Answers a query using grounded generation.

### HTTP request

`POST https://developerknowledge.googleapis.com/v1:answerQuery`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "query": string,
  "filter": string
}
```

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

### Response body

Response message for [`DeveloperKnowledge.AnswerQuery`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#google.developers.knowledge.v1.DeveloperKnowledge.AnswerQuery) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "answer": {
    object (Answer)
  }
}
```

| Fields   |                                                                                                                                           |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `answer` | `object ( `[`Answer`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#Answer)` )` The answer to the query. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

## Answer

An answer to a query.

**JSON representation**

```
{
  "answerText": string,
  "citations": [
    {
      object (AnswerCitation)
    }
  ],
  "references": [
    {
      object (AnswerReference)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                     |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `answerText`   | `string` Contains the text of the answer.                                                                                                                                           |
| `citations[]`  | `object ( `[`AnswerCitation`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerCitation)` )` Output only. Contains citations for the answer.    |
| `references[]` | `object ( `[`AnswerReference`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerReference)` )` Output only. Contains references for the answer. |

## AnswerCitation

Citation info for a segment.

**JSON representation**

```
{
  "startIndex": integer,
  "endIndex": integer,
  "sources": [
    {
      object (CitationSource)
    }
  ]
}
```

| Fields       |                                                                                                                                                                                                                                    |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startIndex` | `integer` Output only. Indicates the start of the segment, measured in bytes (UTF-8 unicode), inclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length. |
| `endIndex`   | `integer` Output only. Indicates the end of the segment, measured in bytes (UTF-8 unicode), exclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.   |
| `sources[]`  | `object ( `[`CitationSource`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#CitationSource)` )` Output only. Contains citation sources for the attributed segment.                                |

## CitationSource

Citation source.

**JSON representation**

```
{
  "referenceIndex": integer
}
```

| Fields           |                                                                                                                                                                                                                 |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `referenceIndex` | `integer` Output only. Contains the index of the [`Answer.AnswerReference`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#AnswerReference) in the `references` repeated field. |

## AnswerReference

Represents a reference to a source.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "documentReference": {
    object (DocumentReference)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                            |                                                                                                                                                                             |
|---------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Contains the content of the reference. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                             |
| `documentReference`                                                                                                                               | `object ( `[`DocumentReference`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#DocumentReference)` )` Output only. The reference document. |
| End of mutually exclusive fields.                                                                                                                 |                                                                                                                                                                             |

## DocumentReference

Represents a reference to a document.

**JSON representation**

```
{
  "documentChunk": {
    object (DocumentChunk)
  }
}
```

| Fields          |                                                                                                                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documentChunk` | `object ( `[`DocumentChunk`](https://developers.google.com/knowledge/reference/rest/v1/DocumentChunk)` )` Output only. Contains the document chunk. The `documentChunk.id` field is not set and will be empty. |
