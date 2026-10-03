---
name: documents/developers.google.com/knowledge/reference/mcp/tools_list/answer_query
uri: https://developers.google.com/knowledge/reference/mcp/tools_list/answer_query
title: 'MCP Tools Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Tool: `answer_query`

Use answer_query to get a grounded answer to a query about Google developer products. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer_query grounds answers using the same corpus as search_documents. This tool returns the generated answer_text and a list of document names (references) used to generate the answer. Use get_documents with the document names to fetch the entire document content if needed.

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
      // provide these details according to the tool's MCP specification
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

| Fields         |                                                                                        |
|----------------|----------------------------------------------------------------------------------------|
| `answerText`   | `string` The answer to the query.                                                      |
| `references[]` | `string` Output only. The resource names of the documents used to generate the answer. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
