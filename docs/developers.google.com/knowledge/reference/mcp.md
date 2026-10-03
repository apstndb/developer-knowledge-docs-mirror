---
name: documents/developers.google.com/knowledge/reference/mcp
uri: https://developers.google.com/knowledge/reference/mcp
title: 'MCP Reference: developerknowledge.googleapis.com'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

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
<li><p>Go: go.dev</p></li>
<li><p>Google AI: ai.google.dev</p></li>
<li><p>Google Antigravity: antigravity.google</p></li>
<li><p>Google Cloud: cloud.google.com &amp; docs.cloud.google.com</p></li>
<li><p>Google Developers, Ads, Search, Google Maps, Youtube: developers.google.com</p></li>
<li><p>Google Home: developers.home.google.com</p></li>
<li><p>Google Maps Platform: mapsplatform.google.com</p></li>
<li><p>TensorFlow: www.tensorflow.org</p></li>
<li><p>Web: web.dev</p></li>
</ul>
<p>This tool returns chunks of text, names, and URLs for matching documents. If the returned chunks are not detailed enough to answer the user's question, use <code>get_documents</code> with the <code>parent</code> from this tool's output to retrieve the full document content.</p></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/knowledge/reference/mcp/tools_list/answer_query"><code>answer_query</code></a></td>
<td><p>Use answer_query to get a grounded answer to a query about Google developer products. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer_query grounds answers using the same corpus as search_documents. This tool returns the generated answer_text and a list of document names (references) used to generate the answer. Use get_documents with the document names to fetch the entire document content if needed.</p>
<p>If you get a 429 out of quota error, use search_documents instead.</p></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/knowledge/reference/mcp/tools_list/get_documents"><code>get_documents</code></a></td>
<td>Use this tool to retrieve the full content of a single document or up to 20 documents in a single call. The document names should be obtained from the <code>parent</code> field of results from a call to the <code>search_documents</code> tool. Set the <code>names</code> parameter to a list of document names.</td>
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
