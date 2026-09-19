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
  - [`AnswerQuery`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery) to get answers to queries grounded in the documentation corpus.

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

A Developer Knowledge API key is required to use the Developer Knowledge API. To create one:

1.  In the Google Cloud console for the project in which you enabled the API, go to the [Credentials page](https://console.cloud.google.com/apis/credentials) .

2.  Click **Create credentials** , and then select **API key** from the menu.

3.  In the **Name** field, provide a name for the key.

4.  Click the **Select API restrictions** drop-down, and then type **Developer Knowledge API** . Click the result, and then click **OK** .
    
    **Notes:**
    
      - If you just enabled the Developer Knowledge API, there may be a delay before it appears in the list. Wait a few minutes and try again.
      - If you plan to use this same key for your AI client's general model calls (for example, `GEMINI_API_KEY` ), you must also select **Generative Language API** . Otherwise, those calls will be blocked.

5.  Click **Create** .

Include this Developer Knowledge API key in your requests. For example, REST calls should include it using the `key` query parameter. Refer to the [Quickstart guide](https://developers.google.com/knowledge/quickstart) for an example.

## Included documentation

Refer to [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) for information about which documents are searched by the API.

The Developer Knowledge API aims to provide access to the latest Google developer documentation. Our goal is to re-index content within 48 hours of publication so that new or updated documentation is available within 2 business days.

## Known limitations

  - **Markdown Quality:** The Markdown is generated from the source HTML. There might be some discrepancies or formatting issues.
  - **Content Scope:** Only public pages on the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) are included. Content from other sources like GitHub, OSS sites, blogs, or YouTube is not included.
