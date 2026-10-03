---
name: documents/developers.google.com/knowledge/api
uri: https://developers.google.com/knowledge/api
title: Developer Knowledge API
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The Developer Knowledge API provides programmatic access to Google's public developer documentation, enabling you to integrate this knowledge base into your own applications and workflows.

## Overview

The Developer Knowledge API is designed to be the canonical source for machine-readable access to Google's developer documentation. It offers functions to search and retrieve documents, and answer queries:

- [`SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rest/v1/documents/searchDocumentChunks) to find relevant page URIs and content snippets based on a query.
- [`GetDocument`](https://developers.google.com/knowledge/reference/rest/v1/documents/get) or [`BatchGetDocuments`](https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet) to fetch the full content of the search result(s).
- [`AnswerQuery`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery) to generate answers to queries drawn from the documentation corpus.

The Developer Knowledge API supports searching and retrieving documentation pages as unstructured Markdown content. The corpus of searchable content is listed in the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) .

### Ways to use Developer Knowledge

You can access Developer Knowledge through the following surfaces depending on your workflow:

- **[REST API](https://developers.google.com/knowledge/quickstart) and [RPC API](https://developers.google.com/knowledge/reference/rpc)** : call the HTTP or gRPC endpoints directly. Refer to the [REST reference](https://developers.google.com/knowledge/reference/rest) and [RPC reference](https://developers.google.com/knowledge/reference/rpc) for method specifications.
- **[Client libraries](https://developers.google.com/knowledge/quickstart-client-libraries)** : integrate the Developer Knowledge API into your applications using official client libraries for Python, Node.js and TypeScript, Go, Java, PHP, and Ruby.
- **[Google Cloud CLI](https://developers.google.com/knowledge/quickstart-gcloud)** ( `gcloud` ): run [`gcloud developer-knowledge` commands](https://docs.cloud.google.com/sdk/gcloud/reference/developer-knowledge) from your terminal to search document chunks, fetch Markdown content, and generate answers.
- **[Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp)** : connect your AI coding assistant or agent to Google's documentation using Model Context Protocol (MCP) tools ( `search_documents` , `get_documents` , and `answer_query` ). Refer to the [MCP reference](https://developers.google.com/knowledge/reference/mcp) .

> **Tip:** If you're using an AI coding assistant, install the [`retrieving-developer-knowledge`](https://github.com/google/skills/tree/main/skills/developers/retrieving-developer-knowledge) agent skill by running `npx skills add google/skills --skill retrieving-developer-knowledge` . This skill gives your assistant built-in instructions on which Developer Knowledge MCP server tool to pick, how to handle errors, and how to call the REST API with `curl` if the MCP server isn't available. To learn more, check out [Use the Developer Knowledge agent skill](https://developers.google.com/knowledge/mcp#agent-skill) .

### Choose between the API and the MCP server

The Developer Knowledge API and the Developer Knowledge MCP server are designed for different integration needs:

- **Use the Developer Knowledge API, client libraries, or gcloud CLI** when:
  - Your project doesn't use an AI agent.
  - You want to define custom tools or tool sets for your agent.
  - You want to process or combine results before passing them to a model (for example, checking document byte length before fetching full content).
  - You need to [filter search results](https://developers.google.com/knowledge/howto#filter-results) (such as by `data_source` or `update_time` ) or apply [field masks](https://developers.google.com/knowledge/howto#field-masks) .
- **Use the Developer Knowledge MCP server and agent skill** when:
  - You want to connect an AI coding assistant or agent without writing custom tool definitions and descriptions.
  - You want automatic updates as the Developer Knowledge MCP server adds new capabilities.
  - You don't need custom metadata filtering on search results.

## Enable the API

To use the Developer Knowledge API, you first need to enable it for your Google Cloud project.

> **Tip:** If you don't have a Google Cloud project, create one using the [Google Cloud](https://developers.google.com/workspace/guides/create-project) or [Firebase](https://firebase.google.com/docs/android/setup#create-firebase-project) instructions.

1.  Open the [Developer Knowledge API page](https://console.cloud.google.com/start/api?id=developerknowledge.googleapis.com) in the Google APIs library.
2.  Check that you have the correct project selected in which you intend to use the API.
3.  Click **Enable** . No specific IAM roles are required to enable or use the API.

## Authentication

You can authenticate requests to the Developer Knowledge API using one of the following methods:

- **API key** : authenticate direct [REST requests](https://developers.google.com/knowledge/quickstart) or the [Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp) using the `key` query parameter or the `X-Goog-Api-Key` header.
- **Application Default Credentials (ADC), OAuth 2.0, or service accounts** : authenticate requests when using the official [client libraries](https://developers.google.com/knowledge/quickstart-client-libraries) or production workflows. To learn more about setting up credentials, refer to the [Application Default Credentials documentation](https://cloud.google.com/docs/authentication/provide-credentials-adc) .
- **User credentials (gcloud CLI)** : authenticate CLI requests by signing in to your Google Cloud account with [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . Refer to the [gcloud CLI quickstart](https://developers.google.com/knowledge/quickstart-gcloud) for setup instructions.

## Included documentation

Refer to [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) for information about which documents are searched by the API.

The Developer Knowledge API aims to provide access to the latest Google developer documentation. Our goal is to re-index content within 48 hours of publication so that new or updated documentation is available within 2 business days.

## Known limitations

- **Markdown Quality:** The Markdown is generated from the source HTML. There might be some discrepancies or formatting issues.
- **Content Scope:** Only public pages on the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) are included. Content from other sources like GitHub, OSS sites, blogs, or YouTube is not included.
