---
name: documents/developers.google.com/knowledge/quota
uri: https://developers.google.com/knowledge/quota
title: Quotas and limits
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

To view your quota and API usage information, go to the [**Quotas & System Limits**](https://console.cloud.google.com/apis/api/developerknowledge.googleapis.com/quotas) page in the Google Cloud console.

The following table lists the default quotas for Developer Knowledge API methods:

| Quota              | API methods                            | Default limit                                                      |
|--------------------|----------------------------------------|--------------------------------------------------------------------|
| Answer generation  | `AnswerQuery`                          | 50 requests per day per project 10 requests per minute per project |
| Search             | `SearchDocumentChunks` , `AnswerQuery` | 100 requests per minute per project (combined)                     |
| Document retrieval | `GetDocument` , `BatchGetDocuments`    | 100 requests per minute per project (combined)                     |

> **Note:** Because `AnswerQuery` searches the corpus before generating an answer, each `AnswerQuery` request consumes one per-minute search request ( `1` quota unit) and one answer generation request ( `2` quota units in the Google Cloud console **Quotas & System Limits** page, where the default limits appear as `100` quota units per day and `20` quota units per minute). If you need to scale both your per-minute burst rate and your daily volume for `AnswerQuery` , request a quota increase for both the per-day and per-minute `answer_query_requests` limits in the Google Cloud console.

For additional information about quotas, visit [View and manage quotas](https://cloud.google.com/docs/quotas/view-manage) .
