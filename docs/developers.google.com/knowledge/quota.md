---
name: documents/developers.google.com/knowledge/quota
uri: https://developers.google.com/knowledge/quota
title: Quotas and limits
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

To view your quota and API usage information, go to the [**Quotas & System Limits**](https://console.cloud.google.com/apis/api/developerknowledge.googleapis.com/quotas) page in the Google Cloud console.

The following table lists the default quotas for Developer Knowledge API methods:

| API method                          | Default quota                         |
| ----------------------------------- | ------------------------------------- |
| `AnswerQuery`                       | 50 per day per project                |
| `GetDocument` , `BatchGetDocuments` | 100 per minute per project (combined) |
| `SearchDocumentChunks`              | 100 per minute per project            |

For additional information about quotas, visit [View and manage quotas](https://cloud.google.com/docs/quotas/view-manage) .
