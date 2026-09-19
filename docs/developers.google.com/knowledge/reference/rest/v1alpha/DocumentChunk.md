---
name: documents/developers.google.com/knowledge/reference/rest/v1alpha/DocumentChunk
uri: https://developers.google.com/knowledge/reference/rest/v1alpha/DocumentChunk
title: DocumentChunk
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1alpha/DocumentChunk#SCHEMA_REPRESENTATION)

A DocumentChunk represents a piece of content from a `  Document  ` in the DeveloperKnowledge corpus. To fetch the entire document content, pass the `parent` to `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;id&quot;: string,&quot;content&quot;: string,&quot;document&quot;: {object (Document)},&quot;relevanceScore&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

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

` object ( Document  ` )

Output only. Represents metadata about the `  Document  ` this chunk is from. The `  DocumentView  ` of this `  Document  ` message will be set to `DOCUMENT_VIEW_BASIC` . It is included here for convenience so that clients do not need to call `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` if they only need the metadata fields. Otherwise, clients should use `  DeveloperKnowledge.GetDocument  ` or `  DeveloperKnowledge.BatchGetDocuments  ` to fetch the full document content.

`relevanceScore`

`number`

Output only. Represents the relevance score of the chunk to the search query. Higher score indicates higher chunk relevance. The score is in range \[0.0, 1.0\].
