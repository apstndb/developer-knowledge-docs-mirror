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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;uri&quot;: string,&quot;content&quot;: string,&quot;description&quot;: string,&quot;dataSource&quot;: string,&quot;title&quot;: string,&quot;updateTime&quot;: string,&quot;view&quot;: enum (DocumentView),&quot;contentLengthBytes&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. Contains the resource name of the document. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

`uri`

`string`

Output only. Provides the URI of the content, such as `https://docs.cloud.google.com/storage/docs/creating-buckets` .

`content`

`string`

Output only. Contains the full content of the document in Markdown format.

`description`

`string`

Output only. Provides a description of the document.

`dataSource`

`string`

Output only. Specifies the data source of the document. Example data source: `firebase.google.com`

`title`

`string`

Output only. Provides the title of the document.

`updateTime`

` string ( Timestamp  ` format)

Output only. Represents the timestamp when the content or metadata of the document was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`view`

` enum ( DocumentView  ` )

Output only. Specifies the `  DocumentView  ` of the document.

`contentLengthBytes`

`integer`

Output only. The length of the `content` field in bytes.

## DocumentView

Specifies which fields of the `  Document  ` are included.

Enums

`DOCUMENT_VIEW_UNSPECIFIED`

The default / unset value. See each API method for its default value if `  DocumentView  ` is not specified.

`DOCUMENT_VIEW_BASIC`

Includes only the basic metadata fields:

  - `name`
  - `uri`
  - `dataSource`
  - `title`
  - `description`
  - `updateTime`
  - `view`
  - `contentLengthBytes`

This is the default of view for `  DeveloperKnowledge.SearchDocumentChunks  ` .

`DOCUMENT_VIEW_FULL`

Includes all `  Document  ` fields.

`DOCUMENT_VIEW_CONTENT`

Includes the `DOCUMENT_VIEW_BASIC` fields and the `content` field.

This is the default of view for `  DeveloperKnowledge.GetDocument  ` and `  DeveloperKnowledge.BatchGetDocuments  ` .

## Methods

### `            batchGet           `

Retrieves multiple documents, each with its full Markdown content.

### `            get           `

Retrieves a single document with its full Markdown content.

### `            searchDocumentChunks           `

Searches for developer knowledge across Google's developer documentation.
