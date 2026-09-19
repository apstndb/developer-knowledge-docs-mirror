---
name: documents/developers.google.com/knowledge/reference/rest/v1alpha/documents/get
uri: https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get
title: 'Method: documents.get'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

  - [HTTP request](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.PATH_PARAMETERS)
  - [Query parameters](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.QUERY_PARAMETERS)
  - [Request body](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.request_body)
  - [Response body](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.response_body)
  - [Authorization scopes](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#body.aspect)
  - [Try it\!](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/get#try-it)

Retrieves a single document with its full Markdown content.

### HTTP request

`GET https://developerknowledge.googleapis.com/v1alpha/{name=documents/**}`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. Specifies the name of the document to retrieve. Format: `documents/{uri_without_scheme}` Example: `documents/docs.cloud.google.com/storage/docs/creating-buckets`

The name must not exceed 500 characters; values longer than 500 characters will result in an `INVALID_ARGUMENT` error.

### Query parameters

Parameters

`view`

` enum ( DocumentView  ` )

Optional. Specifies the `  DocumentView  ` of the document. If unspecified, `  DeveloperKnowledge.GetDocument  ` defaults to `DOCUMENT_VIEW_CONTENT` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Document  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/devprofiles.full_control`
  - `https://www.googleapis.com/auth/developerprofiles.readonly`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [OAuth 2.0 Overview](https://developers.google.com/identity/protocols/OAuth2) .
