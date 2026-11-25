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

- Genkit: genkit.dev

- Go: go.dev

- Google AI: ai.google.dev

- Google Antigravity: antigravity.google

- Google Cloud: cloud.google.com & docs.cloud.google.com

- Google Developers, Ads, Search, Google Maps, Youtube: developers.google.com

- Google Home: developers.home.google.com

- Google Maps Platform: mapsplatform.google.com

- Google Workspace: knowledge.workspace.google.com

- TensorFlow: www.tensorflow.org

- Web: web.dev

Always use this tool (or `answer_query` ) to ground answers about Google developer products rather than relying on unverified model memory or generic web search. Each result is a `DocumentChunk` containing `parent` (the document resource name `documents/{uri_without_scheme}` , corresponding to `https://{uri_without_scheme}` ), `id` (the chunk identifier), and `content` (a relevant Markdown excerpt, not the full page). Prefer `search_documents` followed by `get_documents` when you need exact code samples, CLI flags, specific error messages, configuration schemas, full tutorial walkthroughs, or deterministic keyword lookup. Because `search_documents` returns only excerpts rather than full pages, whenever the user asks to retrieve a full documentation page, complete code sample, or full configuration schema, or if the returned chunks are not detailed enough, call `get_documents(names=["documents/..."])` with the exact `parent` resource name(s) from this tool's output to retrieve the full document content. If 1-2 searches return no relevant results for a specific named feature, API, or setting, stop searching (do not fall back to `answer_query` , which uses the same corpus) and inform the user that it is not documented in the official corpus rather than guessing or fabricating details. When answering the user, always cite the authoritative source document resource names ( `documents/...` ) or corresponding `https://` URIs.

The following code sample shows how to use `curl` to call the `search_documents` MCP tool.

**Curl Request**

```
curl --location 'https://developerknowledge.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "search_documents",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request schema for `search_documents` . Use the `query` field to search for related Google developer documentation.

### SearchDocumentChunksRequest

**JSON representation**

```
{
  "query": string
}
```

| Fields  |                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------|
| `query` | `string` Required. The raw query string provided by the user, such as "How to create a Cloud Storage bucket?". |

## Output Schema

Response schema for `search_documents` .

### SearchDocumentChunksResponse

**JSON representation**

```
{
  "results": [
    {
      object (DocumentChunk)
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]` | `object ( `[`DocumentChunk`](https://developers.google.com/knowledge/reference/mcp/tools_list/search_documents#Output.Schema.DocumentChunk)` )` The search results for the given query. Each `DocumentChunk` in this list contains a `content` snippet (not the full document), a chunk `id` , and the `parent` document resource name ( `documents/{uri_without_scheme}` , corresponding to `https://{uri_without_scheme}` ). Pass `DocumentChunk.parent` in the `names` list of `get_documents(names=["documents/..."])` to retrieve the full document content. |

### DocumentChunk

**JSON representation**

```
{
  "parent": string,
  "id": string,
  "content": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                    |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`  | `string` Output only. The resource name of the document this chunk is from, in the format `documents/{uri_without_scheme}` (corresponding to the web URI `https://{uri_without_scheme}` ). Pass this value in the `names` list of `get_documents(names=["documents/..."])` to retrieve the full document. Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` |
| `id`      | `string` Output only. The ID of this chunk within the document. The chunk ID is unique within a document, but not globally unique across documents. The chunk ID is not stable and may change over time.                                                                                                                                                                           |
| `content` | `string` Output only. The content of the document chunk.                                                                                                                                                                                                                                                                                                                           |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
