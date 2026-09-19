---
name: documents/developers.google.com/knowledge/reference/mcp/tools_list/answer_query
uri: https://developers.google.com/knowledge/reference/mcp/tools_list/answer_query
title: 'MCP Tools Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

## Tool: `answer_query`

Use answer\_query to get a grounded answer to a query about Google developer products. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer\_query grounds answers using the same corpus as search\_documents. This tool returns the generated answer\_text and a list of document names (references) used to generate the answer. Use get\_documents with the document names to fetch the entire document content if needed.

If you get a 429 out of quota error, use search\_documents instead.

The following code sample shows how to use `curl` to call the `answer_query` MCP tool.

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
    &quot;name&quot;: &quot;answer_query&quot;,
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

Request message for `AnswerQuery` .

### AnswerQueryRequest

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

Required. The query to answer.

## Output Schema

Response message for `AnswerQuery` .

### AnswerQueryResponse

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
  &quot;answerText&quot;: string,
  &quot;references&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`answerText`

`string`

The answer to the query.

`references[]`

`string`

Output only. The resource names of the documents used to generate the answer.

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
