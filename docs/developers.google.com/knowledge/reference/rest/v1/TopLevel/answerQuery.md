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
  - [Try it\!](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#try-it)

Answers a query using grounded generation.

### HTTP request

`POST https://developerknowledge.googleapis.com/v1:answerQuery`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;query&quot;: string,
  &quot;filter&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

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

### Response body

Response message for `  DeveloperKnowledge.AnswerQuery  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;answer&quot;: {object (Answer)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`answer`

` object ( Answer  ` )

The answer to the query.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/devprofiles.full_control`
  - `https://www.googleapis.com/auth/developerprofiles.readonly`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .

## Answer

An answer to a query.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;answerText&quot;: string,&quot;citations&quot;: [{object (AnswerCitation)}],&quot;references&quot;: [{object (AnswerReference)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`answerText`

`string`

Contains the text of the answer.

`citations[]`

` object ( AnswerCitation  ` )

Output only. Contains citations for the answer.

`references[]`

` object ( AnswerReference  ` )

Output only. Contains references for the answer.

## AnswerCitation

Citation info for a segment.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;startIndex&quot;: integer,&quot;endIndex&quot;: integer,&quot;sources&quot;: [{object (CitationSource)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`startIndex`

`integer`

Output only. Indicates the start of the segment, measured in bytes (UTF-8 unicode), inclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.

`endIndex`

`integer`

Output only. Indicates the end of the segment, measured in bytes (UTF-8 unicode), exclusive. If there are multi-byte characters, such as non-ASCII characters, the index measurement is longer than the string length.

`sources[]`

` object ( CitationSource  ` )

Output only. Contains citation sources for the attributed segment.

## CitationSource

Citation source.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;referenceIndex&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`referenceIndex`

`integer`

Output only. Contains the index of the `  Answer.AnswerReference  ` in the `references` repeated field.

## AnswerReference

Represents a reference to a source.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// The following is a list of mutually exclusive fields. At most one of the// fields will be set in a response:&quot;documentReference&quot;: {object (DocumentReference)}// End of mutually exclusive fields.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Contains the content of the reference. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`documentReference`

` object ( DocumentReference  ` )

Output only. The reference document.

End of mutually exclusive fields.

## DocumentReference

Represents a reference to a document.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;documentChunk&quot;: {object (DocumentChunk)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`documentChunk`

` object ( DocumentChunk  ` )

Output only. Contains the document chunk. The `documentChunk.id` field is not set and will be empty.
