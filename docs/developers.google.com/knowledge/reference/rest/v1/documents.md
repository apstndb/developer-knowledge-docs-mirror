---
name: documents/developers.google.com/knowledge/reference/rest/v1/documents
uri: https://developers.google.com/knowledge/reference/rest/v1/documents
title: 'REST Resource: documents'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

- [Resource: Document](https://developers.google.com/knowledge/reference/rest/v1/documents#Document)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1/documents#Document.SCHEMA_REPRESENTATION)
- [DocumentView](https://developers.google.com/knowledge/reference/rest/v1/documents#DocumentView)
- [Methods](https://developers.google.com/knowledge/reference/rest/v1/documents#METHODS_SUMMARY)

## Resource: Document

A Document represents a page of documentation in the Developer Knowledge corpus, like the page at <https://docs.cloud.google.com/storage/docs/creating-buckets> .

**JSON representation**

```
{
  "name": string,
  "uri": string,
  "content": string,
  "description": string,
  "dataSource": string,
  "title": string,
  "updateTime": string,
  "view": enum (DocumentView),
  "contentLengthBytes": integer
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Identifier. Contains the resource name of the document. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`                                                                                                                                                                                                                                                                                         |
| `uri`                | `string` Output only. Provides the URI of the content, such as `https://docs.cloud.google.com/storage/docs/creating-buckets` .                                                                                                                                                                                                                                                                                                                                             |
| `content`            | `string` Output only. Contains the full content of the document in Markdown format.                                                                                                                                                                                                                                                                                                                                                                                        |
| `description`        | `string` Output only. Provides a description of the document.                                                                                                                                                                                                                                                                                                                                                                                                              |
| `dataSource`         | `string` Output only. Specifies the data source of the document. Example data source: `firebase.google.com`                                                                                                                                                                                                                                                                                                                                                                |
| `title`              | `string` Output only. Provides the title of the document.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `updateTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Represents the timestamp when the content or metadata of the document was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `view`               | `enum ( `[`DocumentView`](https://developers.google.com/knowledge/reference/rest/v1/documents#DocumentView)` )` Output only. Specifies the [`DocumentView`](https://developers.google.com/knowledge/reference/rest/v1/documents#DocumentView) of the document.                                                                                                                                                                                                             |
| `contentLengthBytes` | `integer` Output only. The length of the `content` field in bytes.                                                                                                                                                                                                                                                                                                                                                                                                         |

## DocumentView

Specifies which fields of the [`Document`](https://developers.google.com/knowledge/reference/rest/v1/documents#Document) are included.

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
<td>The default / unset value. See each API method for its default value if <a href="https://developers.google.com/knowledge/reference/rest/v1/documents#DocumentView"><code>DocumentView</code></a> is not specified.</td>
</tr>
<tr class="even">
<td><code>DOCUMENT_VIEW_BASIC</code></td>
<td><p>Includes only the basic metadata fields:</p>
<ul>
<li><code>name</code></li>
<li><code>uri</code></li>
<li><code>dataSource</code></li>
<li><code>title</code></li>
<li><code>description</code></li>
<li><code>updateTime</code></li>
<li><code>view</code></li>
<li><code>contentLengthBytes</code></li>
</ul>
<p>This is the default of view for <a href="https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks#google.developers.knowledge.v1.DeveloperKnowledge.SearchDocumentChunks"><code>DeveloperKnowledge.SearchDocumentChunks</code></a> .</p></td>
</tr>
<tr class="odd">
<td><code>DOCUMENT_VIEW_FULL</code></td>
<td>Includes all <a href="https://developers.google.com/knowledge/reference/rest/v1/documents#Document"><code>Document</code></a> fields.</td>
</tr>
<tr class="even">
<td><code>DOCUMENT_VIEW_CONTENT</code></td>
<td><p>Includes the <code>DOCUMENT_VIEW_BASIC</code> fields and the <code>content</code> field.</p>
<p>This is the default of view for <a href="https://developers.google.com/knowledge/reference/rest/v1/documents/get#google.developers.knowledge.v1.DeveloperKnowledge.GetDocument"><code>DeveloperKnowledge.GetDocument</code></a> and <a href="https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet#google.developers.knowledge.v1.DeveloperKnowledge.BatchGetDocuments"><code>DeveloperKnowledge.BatchGetDocuments</code></a> .</p></td>
</tr>
</tbody>
</table>

| Methods                                                                                                            |                                                                           |
|--------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| [`batchGet`](https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet)                         | Retrieves multiple documents, each with its full Markdown content.        |
| [`get`](https://developers.google.com/knowledge/reference/rest/v1/documents/get)                                   | Retrieves a single document with its full Markdown content.               |
| [`searchDocumentChunks`](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks) | Searches for developer knowledge across Google's developer documentation. |
