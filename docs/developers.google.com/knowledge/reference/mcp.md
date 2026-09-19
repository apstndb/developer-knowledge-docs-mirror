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

MCP Tools

`  search_documents  `

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

`  answer_query  `

Use answer\_query to get a grounded answer to a query about Google developer products. This tool has limited quota. This tool will synthesize information from the corpus to generate an answer to the query. answer\_query grounds answers using the same corpus as search\_documents. This tool returns the generated answer\_text and a list of document names (references) used to generate the answer. Use get\_documents with the document names to fetch the entire document content if needed.

If you get a 429 out of quota error, use search\_documents instead.

`  get_documents  `

Use this tool to retrieve the full content of a single document or up to 20 documents in a single call. The document names should be obtained from the `parent` field of results from a call to the `search_documents` tool. Set the `names` parameter to a list of document names.

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

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
    &quot;method&quot;: &quot;tools/list&quot;,
    &quot;jsonrpc&quot;: &quot;2.0&quot;,
    &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>
