---
name: documents/developers.google.com/knowledge/reference/mcp/tools_list/search_documents
uri: https://developers.google.com/knowledge/reference/mcp/tools_list/search_documents
title: 'MCP Tools Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Tool: `search_documents`

Use this tool to find documentation about Google developer products. The documents contain official APIs, code snippets, release notes, best practices, guides, debugging info, and more. It covers the following products and domains:

  - ADK: adk.dev

  - Android: developer.android.com

  - Apigee: docs.apigee.com

  - Chrome: developer.chrome.com

  - Dart: dart.dev

  - Firebase: firebase.google.com

  - Flutter: docs.flutter.dev

  - Fuchsia: fuchsia.dev

  - Gemini CLI: geminicli.com

  - Go: go.dev

  - Google AI: ai.google.dev

  - Google Antigravity: antigravity.google

  - Google Cloud: cloud.google.com & docs.cloud.google.com

  - Google Developers, Ads, Search, Google Maps, Youtube: developers.google.com

  - Google Home: developers.home.google.com

  - Google Maps Platform: mapsplatform.google.com

  - TensorFlow: www.tensorflow.org

  - Web: web.dev

This tool returns chunks of text, names, and URLs for matching documents. If the returned chunks are not detailed enough to answer the user's question, use `get_documents` with the `parent` from this tool's output to retrieve the full document content.

The following code sample shows how to use `curl` to call the `search_documents` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>curl --location &#39;https://developerknowledge.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;search_documents&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request schema for search\_documents. Use the query field to search for related Google developer documentation.

### SearchDocumentChunksRequest

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
  &quot;query&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`query`

`string`

Required. The raw query string provided by the user, such as "How to create a Cloud Storage bucket?".

## Output Schema

Response schema for search\_documents.

### SearchDocumentChunksResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (DocumentChunk)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`results[]`

` object ( DocumentChunk  ` )

The search results for the given query. Each Document in this list contains a snippet of content relevant to the search query. Use the DocumentChunk.name field of each result with get\_documents to retrieve the full document content.

### DocumentChunk

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
  &quot;parent&quot;: string,
  &quot;id&quot;: string,
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Output only. The resource name of the document this chunk is from. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

`id`

`string`

Output only. The ID of this chunk within the document. The chunk ID is unique within a document, but not globally unique across documents. The chunk ID is not stable and may change over time.

`content`

`string`

Output only. The content of the document chunk.

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
