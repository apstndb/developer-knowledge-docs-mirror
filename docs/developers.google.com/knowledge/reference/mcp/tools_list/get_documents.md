---
name: documents/developers.google.com/knowledge/reference/mcp/tools_list/get_documents
uri: https://developers.google.com/knowledge/reference/mcp/tools_list/get_documents
title: 'MCP Tools Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Tool: `get_documents`

Use this tool to retrieve the full content of a single document or up to 20 documents in a single call. The document names should be obtained from the `parent` field of results from a call to the `search_documents` tool. Set the `names` parameter to a list of document names.

The following code sample shows how to use `curl` to call the `get_documents` MCP tool.

**Curl Request**

```
curl --location 'https://developerknowledge.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_documents",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request schema for get_documents.

### GetDocumentsRequest

**JSON representation**

```
{
  "names": [
    string
  ]
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                   |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names[]` | `string` Required. The names of the documents to retrieve, as returned by search_documents. A maximum of 20 documents can be retrieved in one call. The documents are returned in the same order as the `names` in the request. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` |

## Output Schema

Response schema for get_documents.

### GetDocumentsResponse

**JSON representation**

```
{
  "documents": [
    {
      object (Document)
    }
  ]
}
```

| Fields        |                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]` | `object ( `[`Document`](https://developers.google.com/knowledge/reference/mcp/tools_list/get_documents#Output.Schema.Document)` )` Documents requested. |

### Document

**JSON representation**

```
{
  "name": string,
  "uri": string,
  "content": string,
  "description": string,
  "title": string
}
```

| Fields        |                                                                                                                                                                           |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`        | `string` Identifier. The resource name of the document. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` |
| `uri`         | `string` Output only. The URI of the content, such as `https://cloud.google.com/storage/docs/creating-buckets` .                                                          |
| `content`     | `string` Output only. The content of the document in Markdown format.                                                                                                     |
| `description` | `string` Output only. A description of the document.                                                                                                                      |
| `title`       | `string` Output only. The title of the document.                                                                                                                          |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
