---
name: documents/developers.google.com/knowledge/reference/rest
uri: https://developers.google.com/knowledge/reference/rest
title: Developer Knowledge API
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The Developer Knowledge API provides access to Google's developer knowledge.

  - [REST Resource: v1alpha](https://developers.google.com/knowledge/reference/rest#v1alpha)
  - [REST Resource: v1alpha.documents](https://developers.google.com/knowledge/reference/rest#v1alpha.documents)
  - [REST Resource: v1](https://developers.google.com/knowledge/reference/rest#v1)
  - [REST Resource: v1.documents](https://developers.google.com/knowledge/reference/rest#v1.documents)

## Service: developerknowledge.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

  - <https://developerknowledge.googleapis.com/$discovery/rest?version=v1>
  - <https://developerknowledge.googleapis.com/$discovery/rest?version=v1alpha>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

  - `https://developerknowledge.googleapis.com`

## REST Resource: [v1alpha](https://developers.google.com/knowledge/reference/rest/v1alpha/TopLevel)

Methods

`  answerQuery  `

`POST /v1alpha:answerQuery`  
Answers a query using grounded generation.

## REST Resource: [v1alpha.documents](https://developers.google.com/knowledge/reference/rest/v1alpha/documents)

Methods

`  batchGet  `

`GET /v1alpha/documents:batchGet`  
Retrieves multiple documents, each with its full Markdown content.

`  get  `

`GET /v1alpha/{name=documents/**}`  
Retrieves a single document with its full Markdown content.

`  searchDocumentChunks  `

`GET /v1alpha/documents:searchDocumentChunks`  
Searches for developer knowledge across Google's developer documentation.

## REST Resource: [v1](https://developers.google.com/knowledge/reference/rest/v1/TopLevel)

Methods

`  answerQuery  `

`POST /v1:answerQuery`  
Answers a query using grounded generation.

## REST Resource: [v1.documents](https://developers.google.com/knowledge/reference/rest/v1/documents)

Methods

`  batchGet  `

`GET /v1/documents:batchGet`  
Retrieves multiple documents, each with its full Markdown content.

`  get  `

`GET /v1/{name=documents/**}`  
Retrieves a single document with its full Markdown content.

`  searchDocumentChunks  `

`GET /v1/documents:searchDocumentChunks`  
Searches for developer knowledge across Google's developer documentation.
