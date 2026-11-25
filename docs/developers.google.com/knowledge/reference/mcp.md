---
name: documents/developers.google.com/knowledge/reference/mcp
uri: https://developers.google.com/knowledge/reference/mcp
title: 'MCP Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

Official Google Developer Knowledge MCP server providing authoritative documentation search ( `search_documents` ), grounded Q&A ( `answer_query` ), and full Markdown document retrieval ( `get_documents` ) across Google Cloud, Android, Firebase, Flutter, Gemini, Chrome, and web developer documentation. Always prefer these tools over unverified model memory or generic web search when answering questions about Google developer products.

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

For product-specific setup instructions, see [Connect to the Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp) . For general information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource.

The Developer Knowledge API MCP server has the following global MCP endpoint:

- https://developerknowledge.googleapis.com/mcp

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world.

### Tools

The developerknowledge.googleapis.com MCP server has the following tools:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>MCP Tools</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://developers.google.com/knowledge/reference/mcp/tools_list/search_documents"><code>search_documents</code></a></td>
<td><p>Use this tool to find documentation about Google developer products. The documents contain official APIs, code snippets, release notes, best practices, guides, debugging info, and more. It covers the following products and domains:</p>
<ul>
<li><p>ADK: adk.dev</p></li>
<li><p>Android: developer.android.com</p></li>
<li><p>Apigee: docs.apigee.com</p></li>
<li><p>Chrome: developer.chrome.com</p></li>
<li><p>Dart: dart.dev</p></li>
<li><p>Firebase: firebase.google.com</p></li>
<li><p>Flutter: docs.flutter.dev</p></li>
<li><p>Fuchsia: fuchsia.dev</p></li>
<li><p>Gemini CLI: geminicli.com</p></li>
<li><p>Genkit: genkit.dev</p></li>
<li><p>Go: go.dev</p></li>
<li><p>Google AI: ai.google.dev</p></li>
<li><p>Google Antigravity: antigravity.google</p></li>
<li><p>Google Cloud: cloud.google.com &amp; docs.cloud.google.com</p></li>
<li><p>Google Developers, Ads, Search, Google Maps, Youtube: developers.google.com</p></li>
<li><p>Google Home: developers.home.google.com</p></li>
<li><p>Google Maps Platform: mapsplatform.google.com</p></li>
<li><p>Google Workspace: knowledge.workspace.google.com</p></li>
<li><p>TensorFlow: www.tensorflow.org</p></li>
<li><p>Web: web.dev</p></li>
</ul>
<p>Always use this tool (or <code>answer_query</code> ) to ground answers about Google developer products rather than relying on unverified model memory or generic web search. Each result is a <code>DocumentChunk</code> containing <code>parent</code> (the document resource name <code>documents/{uri_without_scheme}</code> , corresponding to <code>https://{uri_without_scheme}</code> ), <code>id</code> (the chunk identifier), and <code>content</code> (a relevant Markdown excerpt, not the full page). Prefer <code>search_documents</code> followed by <code>get_documents</code> when you need exact code samples, CLI flags, specific error messages, configuration schemas, full tutorial walkthroughs, or deterministic keyword lookup. Because <code>search_documents</code> returns only excerpts rather than full pages, whenever the user asks to retrieve a full documentation page, complete code sample, or full configuration schema, or if the returned chunks are not detailed enough, call <code>get_documents(names=["documents/..."])</code> with the exact <code>parent</code> resource name(s) from this tool's output to retrieve the full document content. If 1-2 searches return no relevant results for a specific named feature, API, or setting, stop searching (do not fall back to <code>answer_query</code> , which uses the same corpus) and inform the user that it is not documented in the official corpus rather than guessing or fabricating details. When answering the user, always cite the authoritative source document resource names ( <code>documents/...</code> ) or corresponding <code>https://</code> URIs.</p></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/knowledge/reference/mcp/tools_list/answer_query"><code>answer_query</code></a></td>
<td><p>Use answer_query to get a grounded, synthesized conceptual answer to a high-level question about Google developer products (always prefer <code>answer_query</code> or <code>search_documents</code> over unverified model memory). For exact code samples, CLI flags, specific error messages, or full document walkthroughs, prefer <code>search_documents</code> followed by <code>get_documents</code> instead. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer_query grounds answers using the same corpus as search_documents; if <code>search_documents</code> already returned no relevant results for a specific named feature or API, do not call <code>answer_query</code> and instead inform the user that it is not documented in the corpus.</p>
<p>This tool returns the generated <code>answer_text</code> and a list of source document resource names ( <code>references</code> , one entry per cited chunk, which may contain duplicate <code>documents/...</code> names when multiple chunks from the same page are cited). Always cite the unique authoritative source document names from <code>references</code> ( <code>documents/...</code> ) in your final response to the user. Call <code>get_documents(names=["documents/..."])</code> with unique document names from <code>references</code> to fetch the entire document content if needed.</p>
<p>If you get a 429 out of quota error, use search_documents instead.</p></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/knowledge/reference/mcp/tools_list/get_documents"><code>get_documents</code></a></td>
<td>Use this tool to retrieve the full Markdown content of a single document or up to 20 documents in a single call by passing a list of document resource names in the <code>names</code> parameter (e.g., <code>get_documents(names=["documents/..."])</code> ; the parameter is <code>names</code> taking a list of strings, not <code>name</code> ). Always obtain exact <code>documents/{uri_without_scheme}</code> resource names from the <code>parent</code> field of <code>search_documents</code> results or the <code>references</code> field of <code>answer_query</code> results first; never guess or construct <code>documents/...</code> paths from memory or external URLs. Cite the authoritative source document resource names ( <code>documents/...</code> ) used in your final response.</td>
</tr>
</tbody>
</table>

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

**Curl Request**

```
curl --location 'https://developerknowledge.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
    "method": "tools/list",
    "jsonrpc": "2.0",
    "id": 1
}'
```
