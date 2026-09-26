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

In addition to calling the REST API or client libraries directly, you can connect Developer Knowledge to your AI coding assistant using the following tools:

  - **[Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp)** : lets your AI coding assistant search and read Google's documentation using Model Context Protocol (MCP) tools ( `search_documents` , `get_documents` , and `answer_query` ).
  - **[`retrieving-developer-knowledge` agent skill](https://developers.google.com/knowledge/mcp#agent-skill)** : gives your AI assistant built-in instructions on when to use each Developer Knowledge MCP server tool, plus how to call the REST API with `curl` if MCP isn't available.

> **Tip:** If you're setting up an AI coding assistant, you can install the [`retrieving-developer-knowledge`](https://github.com/google/skills/tree/main/skills/developers/retrieving-developer-knowledge) agent skill by running `npx skills add google/skills --skill retrieving-developer-knowledge` .

To get started quickly, follow the [Quickstart guide](https://developers.google.com/knowledge/quickstart) .

The corpus of searchable content is listed in [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) .

The Developer Knowledge API supports searching and retrieving documentation pages as unstructured Markdown content.

## Enable the API

To use the Developer Knowledge API, you first need to enable it for your Google Cloud project.

> **Tip:** If you don't have a Google Cloud project, create one using the [Google Cloud](https://developers.google.com/workspace/guides/create-project) or [Firebase](https://firebase.google.com/docs/android/setup#create-firebase-project) instructions.

1.  Open the [Developer Knowledge API page](https://console.cloud.google.com/start/api?id=developerknowledge.googleapis.com) in the Google APIs library.
2.  Check that you have the correct project selected in which you intend to use the API.
3.  Click **Enable** . No specific IAM roles are required to enable or use the API.

## Authentication

You can authenticate requests to the Developer Knowledge API using one of the following methods:

  - **API key** : authenticate direct REST requests using the `key` query parameter or the `X-Goog-Api-Key` header. Refer to the [REST quickstart](https://developers.google.com/knowledge/quickstart) for an example.
  - **Application Default Credentials (ADC), OAuth 2.0, or service accounts** : authenticate requests when using the official [client libraries](https://developers.google.com/knowledge/quickstart-client-libraries) or production workflows. To learn more about setting up credentials, refer to the [Application Default Credentials documentation](https://cloud.google.com/docs/authentication/provide-credentials-adc) .

## Included documentation

Refer to [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) for information about which documents are searched by the API.

The Developer Knowledge API aims to provide access to the latest Google developer documentation. Our goal is to re-index content within 48 hours of publication so that new or updated documentation is available within 2 business days.

## Known limitations

  - **Markdown Quality:** The Markdown is generated from the source HTML. There might be some discrepancies or formatting issues.
  - **Content Scope:** Only public pages on the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) are included. Content from other sources like GitHub, OSS sites, blogs, or YouTube is not included.
