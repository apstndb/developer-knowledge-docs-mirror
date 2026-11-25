---
name: documents/developers.google.com/knowledge/reference/mcp/tools_list/answer_query
uri: https://developers.google.com/knowledge/reference/mcp/tools_list/answer_query
title: 'MCP Tools Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Tool: `answer_query`

Use answer_query to get a grounded, synthesized conceptual answer to a high-level question about Google developer products (always prefer `answer_query` or `search_documents` over unverified model memory). For exact code samples, CLI flags, specific error messages, or full document walkthroughs, prefer `search_documents` followed by `get_documents` instead. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer_query grounds answers using the same corpus as search_documents; if `search_documents` already returned no relevant results for a specific named feature or API, do not call `answer_query` and instead inform the user that it is not documented in the corpus.

This tool returns the generated `answer_text` and a list of source document resource names ( `references` , one entry per cited chunk, which may contain duplicate `documents/...` names when multiple chunks from the same page are cited). Always cite the unique authoritative source document names from `references` ( `documents/...` ) in your final response to the user. Call `get_documents(names=["documents/..."])` with unique document names from `references` to fetch the entire document content if needed.

If you get a 429 out of quota error, use search_documents instead.

The following code sample shows how to use `curl` to call the `answer_query` MCP tool.

**Curl Request**

```
curl --location 'https://developerknowledge.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "answer_query",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `AnswerQuery` .

### AnswerQueryRequest

**JSON representation**

```
{
  "query": string
}
```

| Fields  |                                         |
|---------|-----------------------------------------|
| `query` | `string` Required. The query to answer. |

## Output Schema

Response message for `AnswerQuery` .

### AnswerQueryResponse

**JSON representation**

```
{
  "answerText": string,
  "references": [
    string
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `answerText`   | `string` The answer to the query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `references[]` | `string` Output only. The resource names of the source documents used to generate the answer (one entry per cited chunk, so the same `documents/{uri_without_scheme}` resource name may appear multiple times when multiple chunks from the same page are cited; e.g., `documents/docs.cloud.google.com/storage/docs/creating-buckets` ). Cite the unique resource names in the final response and pass unique `documents/...` names in the `names` list of `get_documents(names=["documents/..."])` if full document content is needed. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
