---
name: documents/developers.google.com/knowledge/quota
uri: https://developers.google.com/knowledge/quota
title: Quotas and limits
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

To view your quota and API usage information, go to the [**Quotas & System Limits**](https://console.cloud.google.com/apis/api/developerknowledge.googleapis.com/quotas) page in the Google Cloud console.

The following table lists the default quotas for Developer Knowledge API methods:

| Quota              | API methods                            | Default limit                                  |
|--------------------|----------------------------------------|------------------------------------------------|
| Answer generation  | `AnswerQuery`                          | 50 requests per day per project                |
| Search             | `SearchDocumentChunks` , `AnswerQuery` | 100 requests per minute per project (combined) |
| Document retrieval | `GetDocument` , `BatchGetDocuments`    | 100 requests per minute per project (combined) |

> **Note:** Because `AnswerQuery` searches the corpus before generating an answer, each `AnswerQuery` request consumes both one daily answer generation request and one per-minute search request.

For additional information about quotas, visit [View and manage quotas](https://cloud.google.com/docs/quotas/view-manage) .
