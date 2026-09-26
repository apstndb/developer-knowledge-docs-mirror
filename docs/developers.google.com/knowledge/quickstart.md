---
name: documents/developers.google.com/knowledge/quickstart
uri: https://developers.google.com/knowledge/quickstart
title: 'Quickstart: Get started with the Developer Knowledge API'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

This guide shows you how to get started with the Developer Knowledge API. You'll learn how to enable the Developer Knowledge API, get an API key, and make your first API calls to search for and retrieve developer documentation.

## Before you begin

Before you start using the Developer Knowledge API, make sure you complete the following steps.

### Enable the API

1.  Open the [Developer Knowledge API page](https://console.cloud.google.com/start/api?id=developerknowledge.googleapis.com) in the Google APIs library.
2.  Check that you have the correct project selected in which you intend to use the API.
3.  Click **Enable** . No specific IAM roles are required to enable or use the API.

### Create and secure the API key

1.  In the Google Cloud console for the project in which you enabled the API, go to the [Credentials page](https://console.cloud.google.com/apis/credentials) .

2.  Click **Create credentials** , and then select **API key** from the menu.

3.  In the **Name** field, provide a name for the key.

4.  Click the **Select API restrictions** drop-down, and then type **Developer Knowledge API** . Click the result, and then click **OK** .
    
    **Notes:**
    
      - If you just enabled the Developer Knowledge API, there may be a delay before it appears in the list. Wait a few minutes and try again.
      - If you plan to use this same key for your AI client's general model calls (for example, `GEMINI_API_KEY` ), you must also select **Generative Language API** . Otherwise, those calls will be blocked.

5.  Click **Create** .

## Generate answers from documentation

Once you have your Developer Knowledge API key, you can start using the API. The following example shows how to ask a query and generate an answer drawn from the documentation:

1.  Save your Developer Knowledge API key to an environment variable:
    
        export DEVELOPERKNOWLEDGE_API_KEY="YOUR_API_KEY"
    
    Replace `  YOUR_API_KEY  ` with the API key you generated.

2.  Use `curl` to call the `AnswerQuery` endpoint:
    
        curl -X POST "https://developerknowledge.googleapis.com/v1:answerQuery?key=$DEVELOPERKNOWLEDGE_API_KEY" \
          -H "Content-Type: application/json" \
          -d '{"query": "How do I create a BigQuery dataset?"}'

This command returns an answer to your query based on the documentation.

## Search for document chunks

If you want to find specific documentation snippets rather than a generated answer, you can directly search for document chunks.

Use `curl` to call the `SearchDocumentChunks` endpoint:

    curl "https://developerknowledge.googleapis.com/v1/documents:searchDocumentChunks?query=BigQuery&key=$DEVELOPERKNOWLEDGE_API_KEY"

The response includes matching chunks of content from the documentation and references to the parent documents.

## Retrieve a document

The response from `searchDocumentChunks` contains a list of document chunks. Each document chunk has a `parent` field containing the resource name of the document, which you can use with `GetDocument` to retrieve the document's full content.

To retrieve a document, copy the `parent` field from one of the chunks returned by `searchDocumentChunks` and save it to an environment variable, then use `curl` to call the `GetDocument` endpoint:

    export DOC_NAME="PARENT_FIELD_FROM_SEARCH"

    curl "https://developerknowledge.googleapis.com/v1/$DOC_NAME?key=$DEVELOPERKNOWLEDGE_API_KEY"

This returns the full Markdown content of the specified document.

## What's next

  - [Connect to the Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp) and install the [`retrieving-developer-knowledge` agent skill](https://developers.google.com/knowledge/mcp#agent-skill) to help your AI coding assistant search official Google documentation.
  - Explore the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) to view the full list of included documentation.
  - Refer to the [API reference documentation](https://developers.google.com/knowledge/reference/rest) for more details on API methods and parameters.
  - Learn how to [set up the MCP server in Google Antigravity](https://codelabs.developers.google.com/developer-knowledge-mcp-antigravity) .
