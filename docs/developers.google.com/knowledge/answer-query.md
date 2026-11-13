---
name: documents/developers.google.com/knowledge/answer-query
uri: https://developers.google.com/knowledge/answer-query
title: Generate answers from documentation
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The Developer Knowledge API lets you ask questions about Google developer products and receive direct, natural-language answers. For each query, the API composes a response drawn from the [Developer Knowledge corpus](https://developers.google.com/knowledge/reference/corpus-reference) (referred to in the API reference as *grounded generation* ) and includes citations to the relevant documentation pages.

## Before you begin

Set up your environment for your preferred tool:

### gcloud

[Install and configure the gcloud CLI, and enable the Developer Knowledge API](https://developers.google.com/knowledge/quickstart-gcloud#before-you-begin) .

### REST

[Enable the API and generate a Developer Knowledge API key](https://developers.google.com/knowledge/quickstart#before-you-begin) . Then, save your key to an environment variable:

```
export DEVELOPERKNOWLEDGE_API_KEY="YOUR_API_KEY"
```

Replace `YOUR_API_KEY` with your Developer Knowledge API key.

## Answer a query

Use the [`gcloud developer-knowledge answer-query` command](https://docs.cloud.google.com/sdk/gcloud/reference/developer-knowledge/answer-query) or the [`answerQuery`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery) REST method to ask a question.

The following example sends a query asking how to create a BigQuery dataset:

### gcloud

```
gcloud developer-knowledge answer-query \
  --query="How do I create a BigQuery dataset?"
```

### REST

```
curl -X POST "https://developerknowledge.googleapis.com/v1:answerQuery?key=$DEVELOPERKNOWLEDGE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "How do I create a BigQuery dataset?"}'
```

The response contains the text answer in the `answer.answerText` field, along with `citations` and `references` in the [`answer`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#answer) object:

```
{
  "answer": {
    "answerText": "To create a BigQuery dataset, you can use the Google Cloud console, the bq command-line tool, or the BigQuery client libraries.",
    "citations": [
      {
        "startIndex": 0,
        "endIndex": 123,
        "sources": [
          {
            "referenceIndex": 0
          }
        ]
      }
    ],
    "references": [
      {
        "documentReference": {
          "documentChunk": {
            "parent": "documents/docs.cloud.google.com/bigquery/docs/datasets",
            "content": "This page explains how to create BigQuery datasets...",
            "document": {
              "name": "documents/docs.cloud.google.com/bigquery/docs/datasets",
              "title": "Introduction to datasets",
              "uri": "https://docs.cloud.google.com/bigquery/docs/datasets"
            }
          }
        }
      }
    ]
  }
}
```

## Filter documentation sources

To restrict the documentation sources used to generate the answer, pass a filter expression using the `--query-filter` flag in the gcloud CLI or the `filter` field in your REST request body. For details on supported filter fields and operators, see [Filter search results](https://developers.google.com/knowledge/search-retrieve#filter-results) .

The following example restricts the documentation sources to `docs.cloud.google.com` :

### gcloud

```
gcloud developer-knowledge answer-query \
  --query="How do I create a BigQuery dataset?" \
  --query-filter='data_source = "docs.cloud.google.com"'
```

### REST

```
curl -X POST "https://developerknowledge.googleapis.com/v1:answerQuery?key=$DEVELOPERKNOWLEDGE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "How do I create a BigQuery dataset?",
    "filter": "data_source = \"docs.cloud.google.com\""
  }'
```

## Choose between `AnswerQuery` and `SearchDocumentChunks`

When you're using the API or the Developer Knowledge MCP server, choose the method that best fits what you're looking for:

- **`AnswerQuery` (or the `answer_query` MCP tool)** : best for general "how-to" questions, comparing products, and step-by-step guides where you want a complete summary with links to the source docs.
- **`SearchDocumentChunks` (or the `search_documents` MCP tool)** : best for looking up exact CLI flags, code syntax, parameter names, or IAM permissions (such as `service.resource.verb` ). Use two to five specific keywords instead of a full question.

> **Tip:** Install the [`retrieving-developer-knowledge`](https://developers.google.com/knowledge/mcp#agent-skill) agent skill in your AI coding assistant so it automatically picks the right tool for your question.

## Parse citations and references

When you call `answerQuery` , the `answer` object provides fine-grained attribution that links specific segments of the generated `answerText` to source passages in `references` .

A single source document in `references` can be cited multiple times across different text segments, and a single segment can cite multiple references.

### Example response with citations

The following JSON snippet illustrates an `answer` object with multiple citations pointing to different documentation references:

```
{
  "answer": {
    "answerText": "You can create a BigQuery dataset using the Google Cloud console, the bq command-line tool, or the client libraries. Each dataset is assigned a region or multi-region location when created.",
    "citations": [
      {
        "startIndex": 0,
        "endIndex": 116,
        "sources": [
          {
            "referenceIndex": 0
          }
        ]
      },
      {
        "startIndex": 117,
        "endIndex": 189,
        "sources": [
          {
            "referenceIndex": 1
          }
        ]
      }
    ],
    "references": [
      {
        "documentReference": {
          "documentChunk": {
            "parent": "documents/docs.cloud.google.com/bigquery/docs/datasets",
            "content": "You can create a dataset in BigQuery using the Google Cloud console, the bq command-line tool, or client libraries...",
            "document": {
              "name": "documents/docs.cloud.google.com/bigquery/docs/datasets",
              "title": "Creating and managing datasets",
              "uri": "https://docs.cloud.google.com/bigquery/docs/datasets"
            }
          }
        }
      },
      {
        "documentReference": {
          "documentChunk": {
            "parent": "documents/docs.cloud.google.com/bigquery/docs/locations",
            "content": "When you create a dataset, you specify the location where your BigQuery data is stored...",
            "document": {
              "name": "documents/docs.cloud.google.com/bigquery/docs/locations",
              "title": "Dataset locations",
              "uri": "https://docs.cloud.google.com/bigquery/docs/locations"
            }
          }
        }
      }
    ]
  }
}
```

### Citation mapping and fields

To map citations to their documentation sources, use the following fields:

- `answerText` : the complete generated, natural-language response string.
- `citations` : an array of cited segment attributions:
  - `startIndex` : the inclusive starting offset of the cited segment, measured in UTF-8 bytes.
  - `endIndex` : the exclusive ending offset of the cited segment, measured in UTF-8 bytes.
  - `sources` : an array of citation sources. Each entry contains a 0-based `referenceIndex` that corresponds to an item in the `references` array (for example, `referenceIndex: 0` maps to `references[0]` ).
- `references` : an array of source document passages used to generate the answer. Each entry contains a `documentReference.documentChunk` with the following metadata:
  - `document.title` : the title of the documentation page.
  - `document.uri` : the public URL of the documentation page.
  - `document.name` : the canonical resource name of the document.
  - `content` : the extracted text snippet from the document chunk used to synthesize the answer.
  - `parent` : the resource name of the parent document (for example, `documents/docs.cloud.google.com/bigquery/docs/datasets` ), which you can pass to [`documents.get`](https://developers.google.com/knowledge/reference/rest/v1/documents/get) or [`documents.batchGet`](https://developers.google.com/knowledge/reference/rest/v1/documents/batchGet) to retrieve the full document.

### Implement citations in your application

To render answers with citations in client applications or AI agent pipelines:

1.  **Extract cited segments:** to slice the relevant span from `answerText` , use the `startIndex` and `endIndex` byte offsets.
2.  **Resolve source details:** to retrieve the page `document.title` and destination `document.uri` , look up the corresponding item in `references` using `sources[].referenceIndex` .
3.  **Render inline links or footnotes:** to link directly to the source page, insert footnote numbers (such as `[1]` or `[2]` ), preview cards, or clickable hyperlinks pointing to `document.uri` .
4.  **Fetch full context if needed:** to fetch the complete documentation page when the excerpt in `content` is insufficient, pass `parent` to [`documents.get`](https://developers.google.com/knowledge/reference/rest/v1/documents/get) .

> **Note:** `startIndex` and `endIndex` are measured in **UTF-8 bytes** , not character counts or UTF-16 code units. To avoid offset errors with multi-byte characters or emoji, slice `answerText` based on how your programming language indexes strings:

- **UTF-16 languages (JavaScript or TypeScript):** convert the string to UTF-8 bytes before slicing. For example, use `Buffer.from(answerText, 'utf-8').subarray(start, end)` in Node.js, or `TextEncoder` and `TextDecoder` in browser environments.
- **Python:** encode the string to UTF-8 bytes before slicing, and then decode: `answer_text.encode('utf-8')[start:end].decode('utf-8')` .
- **Other languages:** for languages that index strings by UTF-8 bytes natively (such as Go or Rust), slice `answerText` directly using `startIndex` and `endIndex` . Otherwise, convert the string to UTF-8 bytes before slicing.

## What's next

- [Search and retrieve documents](https://developers.google.com/knowledge/search-retrieve) to fetch matching text snippets or full Markdown pages.
- [Connect to the Developer Knowledge MCP server](https://developers.google.com/knowledge/mcp) and install the [`retrieving-developer-knowledge` agent skill](https://developers.google.com/knowledge/mcp#agent-skill) .
- Browse the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) to view all supported documentation sources.
