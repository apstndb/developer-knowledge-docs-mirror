---
name: documents/developers.google.com/knowledge/answer-query
uri: https://developers.google.com/knowledge/answer-query
title: Answer queries with grounded generation
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

Use the `AnswerQuery` method to get answers to queries that are grounded in the [Developer Knowledge corpus](https://developers.google.com/knowledge/reference/corpus-reference) .

## Before you begin

Make sure you have [enabled the API and generated a Developer Knowledge API key](https://developers.google.com/knowledge/api#authentication) , and save your key to an environment variable:

    export DEVELOPERKNOWLEDGE_API_KEY="YOUR_API_KEY"

## Example usage

The following example asks "How do I create a BigQuery dataset?":

    curl -X POST "https://developerknowledge.googleapis.com/v1:answerQuery?key=$DEVELOPERKNOWLEDGE_API_KEY" \
      -H "Content-Type: application/json" \
      -d '{"query": "How do I create a BigQuery dataset?"}'

The response contains the text answer in the `answer.answer_text` field, along with `citations` and `references` in the [`answer`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#answer) object:

    {
      "answer": {
        "answerText": "To create a BigQuery dataset, you can use the Google Cloud Console, the bq command-line tool, or the BigQuery client libraries.",
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
                "parent": "documents/cloud.google.com/bigquery/docs/datasets",
                "content": "This page explains how to create BigQuery datasets...",
                "document": {
                  "name": "documents/cloud.google.com/bigquery/docs/datasets",
                  "title": "Introduction to datasets",
                  "uri": "https://cloud.google.com/bigquery/docs/datasets"
                }
              }
            }
          }
        ]
      }
    }
