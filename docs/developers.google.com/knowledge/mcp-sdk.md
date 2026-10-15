---
name: documents/developers.google.com/knowledge/mcp-sdk
uri: https://developers.google.com/knowledge/mcp-sdk
title: Connect to the Developer Knowledge MCP server using MCP SDKs
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The official [Model Context Protocol (MCP) SDKs](https://modelcontextprotocol.io/docs/sdk) let your own applications and AI agents connect to the Developer Knowledge MCP server programmatically. Use an MCP SDK when you're building a custom agent, a backend service, or your own MCP server that needs to search and retrieve official Google developer documentation, rather than configuring an existing IDE or coding assistant.

In this guide, you learn how to:

- Install the MCP client SDK for Python or TypeScript.
- Connect to the Developer Knowledge MCP server with an API key or Application Default Credentials (ADC).
- Call the `search_documents` , `get_documents` , and `answer_query` tools.
- Handle authentication, quota, and tool errors.

> **Note:** To connect an IDE or coding assistant such as Google Antigravity, Claude Code, or Cursor, refer to [Connect to the Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp) instead.

## Before you begin

Before you start, complete the following sections.

### Enable the API and create credentials

Enable the Developer Knowledge API in your Google Cloud project and create the credentials for your authentication method. For step-by-step instructions, refer to [Choose your authentication method](https://developers.google.com/knowledge/mcp#choose-auth) .

The examples in this guide use an API key. To use ADC instead, refer to [Authenticate with Application Default Credentials](https://developers.google.com/knowledge/mcp-sdk#adc) .

### Install the MCP SDK

Select your programming language to install the MCP client SDK:

### Python

This guide uses version 2 of the [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) , which requires Python 3.10 or later. Version 1.x of the SDK uses different class and function names, so these examples don't work with it:

```
pip install --upgrade "mcp>=2"
```

### TypeScript

This guide uses the [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) with Node.js 18 or later:

```
npm install @modelcontextprotocol/sdk
```

### Set your API key

To avoid hardcoding your API key in source code, store it in an environment variable. Replace ` YOUR_API_KEY ` with your API key:

```
export DEVELOPERKNOWLEDGE_API_KEY="YOUR_API_KEY"
```

## Connect to the server

The Developer Knowledge MCP server uses the [Streamable HTTP transport](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports#streamable-http) at the following endpoint:

```
https://developerknowledge.googleapis.com/mcp
```

To authenticate, pass your API key in the `X-Goog-Api-Key` HTTP header on every request. Don't pass the API key as a URL query parameter.

The following example connects to the server and lists the available tools:

### Python

```
import asyncio
import os

from mcp import Client
from mcp.client.streamable_http import (
    create_mcp_http_client,
    streamable_http_client,
)

MCP_URL = "https://developerknowledge.googleapis.com/mcp"

async def main() -> None:
    headers = {"X-Goog-Api-Key": os.environ["DEVELOPERKNOWLEDGE_API_KEY"]}

    async with create_mcp_http_client(headers=headers) as http_client:
        transport = streamable_http_client(MCP_URL, http_client=http_client)
        async with Client(transport) as client:
            tools = await client.list_tools()
            names = ", ".join(tool.name for tool in tools.tools)
            print("Available tools:", names)

if __name__ == "__main__":
    asyncio.run(main())
```

### TypeScript

```
import { Client } from '@modelcontextprotocol/sdk/client/index.js';
import {
  StreamableHTTPClientTransport,
} from '@modelcontextprotocol/sdk/client/streamableHttp.js';

const apiKey = process.env.DEVELOPERKNOWLEDGE_API_KEY;
if (!apiKey) {
  throw new Error('Set the DEVELOPERKNOWLEDGE_API_KEY variable.');
}

const transport = new StreamableHTTPClientTransport(
  new URL('https://developerknowledge.googleapis.com/mcp'),
  { requestInit: { headers: { 'X-Goog-Api-Key': apiKey } } },
);

const client = new Client({ name: 'my-docs-agent', version: '1.0.0' });
await client.connect(transport);

const { tools } = await client.listTools();
console.log('Available tools:', tools.map((tool) => tool.name).join(', '));

await client.close();
```

If the connection succeeds, the output lists the three tools:

```
Available tools: search_documents, answer_query, get_documents
```

The remaining examples in this guide run inside the connected client from this section. The TypeScript examples use top-level `await` , so run them as ES modules (for example, with `npx tsx index.ts` ).

## Call the tools

Each tool returns its result as structured content that matches the tool's output schema, so you can read fields directly instead of parsing text. For the full input and output schemas, refer to the [MCP reference](https://developers.google.com/knowledge/reference/mcp) .

### Search for documentation

Call `search_documents` with a `query` string to retrieve the most relevant documentation chunks. Each result contains the chunk `content` and the `parent` resource name of the document it came from:

### Python

```
search = await client.call_tool(
    "search_documents",
    {"query": "How do I create a Cloud Storage bucket?"},
)
results = search.structured_content["results"]
for chunk in results[:3]:
    print(f"{chunk['parent']}\n{chunk['content'][:200]}...\n")
```

### TypeScript

```
const search = await client.callTool({
  name: 'search_documents',
  arguments: { query: 'How do I create a Cloud Storage bucket?' },
});
const { results } = search.structuredContent as {
  results: { parent: string; id: string; content: string }[];
};
for (const chunk of results.slice(0, 3)) {
  console.log(`${chunk.parent}\n${chunk.content.slice(0, 200)}...\n`);
}
```

### Retrieve full documents

If a chunk doesn't contain enough context, pass one or more `parent` values to `get_documents` to retrieve the full Markdown content of each page. You can request up to 20 documents in a single call. Because several chunks can come from the same document, remove duplicate `parent` values first:

### Python

```
names = list(dict.fromkeys(chunk["parent"] for chunk in results[:3]))
get = await client.call_tool("get_documents", {"names": names})
for document in get.structured_content["documents"]:
    print(f"{document['title']} ({document['uri']})")
    print(document["content"])
```

### TypeScript

```
const names = [...new Set(results.slice(0, 3).map((c) => c.parent))];
const get = await client.callTool({
  name: 'get_documents',
  arguments: { names },
});
const { documents } = get.structuredContent as {
  documents: {
    name: string;
    uri: string;
    title: string;
    content: string;
  }[];
};
for (const document of documents) {
  console.log(`${document.title} (${document.uri})`);
  console.log(document.content);
}
```

Full documents can be large, so call `get_documents` only when the search chunks aren't sufficient. To learn more, refer to [Optimize context window and token usage](https://developers.google.com/knowledge/mcp#manage-token-usage) .

### Generate an answer

Call `answer_query` to generate an answer grounded in the [Developer Knowledge corpus](https://developers.google.com/knowledge/reference/corpus-reference) . The result contains the `answerText` and the `references` used to generate it:

### Python

```
answer = await client.call_tool(
    "answer_query",
    {"query": "How do I create a Cloud Storage bucket?"},
)
print(answer.structured_content["answerText"])
for reference in answer.structured_content["references"]:
    print(reference)
```

### TypeScript

```
const answer = await client.callTool({
  name: 'answer_query',
  arguments: { query: 'How do I create a Cloud Storage bucket?' },
});
const { answerText, references } = answer.structuredContent as {
  answerText: string;
  references: string[];
};
console.log(answerText);
console.log(references.join('\n'));
```

The `references` field contains document resource names that you can pass to `get_documents` . The same document can appear more than once, so remove duplicates before you retrieve the documents. The `answer_query` tool has a lower quota than the other tools. To learn more, refer to [Quota and limits](https://developers.google.com/knowledge/quota) .

## Authenticate with Application Default Credentials

Instead of an API key, you can authenticate with [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) . ADC works with your user credentials during local development and with service accounts when your code runs on Google Cloud.

When you use ADC, send the following headers on every request:

- `Authorization` : a `Bearer` OAuth 2.0 access token with the `https://www.googleapis.com/auth/cloud-platform` scope.
- `X-Goog-User-Project` : the ID of the project that has the Developer Knowledge API enabled and is billed for quota. Your account needs the `serviceusage.services.use` permission on this project.

Access tokens expire, so long-running clients must refresh them. The following examples use the Google authentication libraries to add a current token to each request.

1.  Set up ADC for local development by following the steps on the **ADC** tab in [Choose your OAuth credential type](https://developers.google.com/knowledge/mcp#oauth-types) .

2.  Set the `GOOGLE_CLOUD_PROJECT` environment variable to the project that has the Developer Knowledge API enabled. The examples send this project ID in the `X-Goog-User-Project` header:

    ```
    export GOOGLE_CLOUD_PROJECT="PROJECT_ID"
    ```

3.  Install the Google authentication library for your language:

    ### Python

    ```
    pip install --upgrade google-auth requests
    ```

    ### TypeScript

    ```
    npm install google-auth-library
    ```

4.  Create the client with ADC:

    ### Python

    ```
    import os

    import google.auth
    import google.auth.transport.requests
    import httpx2  # Installed automatically with mcp>=2
    from mcp import Client
    from mcp.client.streamable_http import (
        create_mcp_http_client,
        streamable_http_client,
    )

    MCP_URL = "https://developerknowledge.googleapis.com/mcp"

    class GoogleCredentialsAuth(httpx2.Auth):
        """Adds a current ADC access token and quota project to requests."""

        def __init__(self, project_id: str) -> None:
            self.credentials, _ = google.auth.default(
                scopes=["https://www.googleapis.com/auth/cloud-platform"]
            )
            self.project_id = project_id

        def auth_flow(self, request):
            if not self.credentials.valid:
                self.credentials.refresh(
                    google.auth.transport.requests.Request()
                )
            request.headers["Authorization"] = (
                f"Bearer {self.credentials.token}"
            )
            request.headers["X-Goog-User-Project"] = self.project_id
            yield request

    async def main() -> None:
        auth = GoogleCredentialsAuth(os.environ["GOOGLE_CLOUD_PROJECT"])
        async with create_mcp_http_client(auth=auth) as http_client:
            transport = streamable_http_client(
                MCP_URL, http_client=http_client
            )
            async with Client(transport) as client:
                ...
    ```

    ### TypeScript

    ```
    import { GoogleAuth } from 'google-auth-library';
    import { Client } from '@modelcontextprotocol/sdk/client/index.js';
    import {
      StreamableHTTPClientTransport,
    } from '@modelcontextprotocol/sdk/client/streamableHttp.js';

    const auth = new GoogleAuth({
      scopes: 'https://www.googleapis.com/auth/cloud-platform',
    });
    const projectId = process.env.GOOGLE_CLOUD_PROJECT;
    if (!projectId) {
      throw new Error('Set the GOOGLE_CLOUD_PROJECT variable.');
    }

    const transport = new StreamableHTTPClientTransport(
      new URL('https://developerknowledge.googleapis.com/mcp'),
      {
        // Add a current access token and the quota project to each request.
        fetch: async (url, init) => {
          const headers = new Headers(init?.headers);
          for (const [name, value] of await auth.getRequestHeaders()) {
            headers.set(name, value);
          }
          headers.set('X-Goog-User-Project', projectId);
          return fetch(url, { ...init, headers });
        },
      },
    );

    const client = new Client({ name: 'my-docs-agent', version: '1.0.0' });
    await client.connect(transport);
    ```

## Handle errors

Errors from the Developer Knowledge MCP server reach your code in two ways:

- **Request errors** : authentication, permission, and quota errors are returned with an HTTP error status, such as `400` , `403` , or `429` . The SDKs raise these as exceptions: `MCPError` in Python and `StreamableHTTPError` in TypeScript. Catch these exceptions around your tool calls.
- **Tool errors** : when a tool runs but can't complete the request, the result has `is_error` (Python) or `isError` (TypeScript) set to `true` , and the `content` field contains a text description of the problem. Check this field before reading the structured content.

The following example handles both error types:

### Python

```
from mcp import MCPError

try:
    result = await client.call_tool(
        "search_documents", {"query": "Cloud Storage buckets"}
    )
except MCPError as error:
    print(f"Request failed ({error.code}): {error.message}")
else:
    if result.is_error:
        print("Tool error:", result.content)
    else:
        results = result.structured_content["results"]
```

### TypeScript

```
import {
  StreamableHTTPError,
} from '@modelcontextprotocol/sdk/client/streamableHttp.js';

try {
  const result = await client.callTool({
    name: 'search_documents',
    arguments: { query: 'Cloud Storage buckets' },
  });
  if (result.isError) {
    console.error('Tool error:', result.content);
  } else {
    const { results } = result.structuredContent as {
      results: { parent: string; id: string; content: string }[];
    };
  }
} catch (error) {
  if (error instanceof StreamableHTTPError) {
    console.error(`Request failed (${error.code}): ${error.message}`);
  } else {
    throw error;
  }
}
```

If `answer_query` returns a quota error ( `429 RESOURCE_EXHAUSTED` ), fall back to `search_documents` , which has a higher quota. For retry strategies, including exponential backoff, refer to [Error handling and quota management](https://developers.google.com/knowledge/error-handling-and-limits) . For common causes of authentication errors, refer to [API key errors](https://developers.google.com/knowledge/mcp#api-key-errors) and [OAuth and ADC errors](https://developers.google.com/knowledge/mcp#resolve-auth-errors) .

## What's next

- Explore the full tool schemas in the [MCP reference](https://developers.google.com/knowledge/reference/mcp) .
- Learn which products are indexed in the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) .
- Call the Developer Knowledge API directly with the [client libraries](https://developers.google.com/knowledge/quickstart-client-libraries) .
