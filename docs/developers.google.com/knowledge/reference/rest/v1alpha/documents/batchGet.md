---
name: documents/developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet
uri: https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet
title: 'Method: documents.batchGet'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

- [HTTP request](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.HTTP_TEMPLATE)
- [Query parameters](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.QUERY_PARAMETERS)
- [Request body](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.request_body)
- [Response body](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.response_body)
  - [JSON representation](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.BatchGetDocumentsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#body.aspect)
- [Try it!](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#try-it)

Retrieves multiple documents, each with its full Markdown content.

### HTTP request

`GET https://developerknowledge.googleapis.com/v1alpha/documents:batchGet`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Query parameters

| Parameters |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names[]`  | `string` Required. Specifies the names of the documents to retrieve. A maximum of 20 documents can be retrieved in a batch. The documents are returned in the same order as the `names` in the request. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets` Each name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.                                                                                |
| `view`     | `enum ( `[`DocumentView`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents#DocumentView)` )` Optional. Specifies the [`DocumentView`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents#DocumentView) of the document. If unspecified, [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) defaults to `DOCUMENT_VIEW_CONTENT` . |

### Request body

The request body must be empty.

### Response body

Response message for [`DeveloperKnowledge.BatchGetDocuments`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/batchGet#google.developers.knowledge.v1alpha.DeveloperKnowledge.BatchGetDocuments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "documents": [
    {
      object (Document)
    }
  ]
}
```

| Fields        |                                                                                                                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]` | `object ( `[`Document`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents#Document)` )` Contains the documents requested. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/devprofiles.full_control`
- `https://www.googleapis.com/auth/developerprofiles.readonly`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .
