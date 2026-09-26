---
name: documents/developers.google.com/knowledge/release-notes
uri: https://developers.google.com/knowledge/release-notes
title: Release notes
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

This page provides information about updates to the Developer Knowledge API and Developer Knowledge MCP server. Check this page for announcements about new or updated features, bug fixes, and known issues.

## September 25, 2026

  - add\_circle The [`retrieving-developer-knowledge`](https://github.com/google/skills/tree/main/skills/developers/retrieving-developer-knowledge) agent skill is now available in the [`google/skills`](https://github.com/google/skills) repository, which helps AI coding assistants choose the right Developer Knowledge MCP server tool and fall back to the REST API when MCP is unavailable. For more information, see [Use the Developer Knowledge agent skill](https://developers.google.com/knowledge/mcp#agent-skill) .

## September 22, 2026

  - add\_circle [`gcloud developer-knowledge`](https://cloud.google.com/sdk/gcloud/reference/developer-knowledge) commands are generally available (GA) in the [`gcloud` CLI](https://cloud.google.com/sdk) .
      - [`gcloud developer-knowledge answer-query`](https://cloud.google.com/sdk/gcloud/reference/developer-knowledge/answer-query) : Generate answers to queries drawn from developer documentation.
      - [`gcloud developer-knowledge documents describe`](https://cloud.google.com/sdk/gcloud/reference/developer-knowledge/documents/describe) : Retrieve document metadata and content views.
      - [`gcloud developer-knowledge documents search-chunks`](https://cloud.google.com/sdk/gcloud/reference/developer-knowledge/documents/search-chunks) : Search relevant document chunks for a given query.

## September 9, 2026

  - add\_circle [`gcloud beta developer-knowledge`](https://cloud.google.com/sdk/gcloud/reference/beta/developer-knowledge) commands are available in the 'beta' component of the [`gcloud` CLI](https://cloud.google.com/sdk) .
      - [`gcloud beta developer-knowledge answer-query`](https://cloud.google.com/sdk/gcloud/reference/beta/developer-knowledge/answer-query) : Generate answers to queries drawn from developer documentation.
      - [`gcloud beta developer-knowledge documents describe`](https://cloud.google.com/sdk/gcloud/reference/beta/developer-knowledge/documents/describe) : Retrieve document metadata and content views.
      - [`gcloud beta developer-knowledge documents search-chunks`](https://cloud.google.com/sdk/gcloud/reference/beta/developer-knowledge/documents/search-chunks) : Search relevant document chunks for a given query.

## August 27, 2026

  - add\_circle Filtering is now generally available (GA) in the v1 API for `AnswerQueryRequest` . For more information, see the reference for [`AnswerQueryRequest.filter`](https://developers.google.com/knowledge/reference/rest/v1/TopLevel/answerQuery#body.request_body.FIELDS.filter) .

## August 25, 2026

  - add\_circle The following domain is now included in the corpus:
    
      - [genkit.dev](https://genkit.dev)
    
    See the full list of supported domains in the [Corpus Reference](https://developers.google.com/knowledge/reference/corpus-reference) .

## August 21, 2026

  - add\_circle `DocumentChunk` messages in the v1 API now include a `relevance_score` field in the range `[0.0, 1.0]` , indicating the chunk's relevance to `AnswerQuery` or `SearchDocumentChunks` queries.

## August 18, 2026

  - add\_circle (v1alpha) [`gcloud alpha developer-knowledge`](https://cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge) commands are available in the 'alpha' component of the [`gcloud` CLI](https://cloud.google.com/sdk) .
      - [`gcloud alpha developer-knowledge answer-query`](https://cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/answer-query) : Generate answers to queries drawn from developer documentation.
      - [`gcloud alpha developer-knowledge documents describe`](https://cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe) : Retrieve document metadata and content views.
      - [`gcloud alpha developer-knowledge documents search-chunks`](https://cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/search-chunks) : Search relevant document chunks for a given query.

## August 7, 2026

  - add\_circle (v1alpha) `DocumentChunk` messages now include a `relevance_score` field in the range `[0.0, 1.0]` , indicating the chunk's relevance to `AnswerQuery` or `SearchDocumentChunks` queries.
  - add\_circle (v1alpha) `AnswerQueryRequest` now supports filtering search results using the `filter` field. For more information, see the reference for [`AnswerQueryRequest.filter`](https://developers.google.com/knowledge/reference/rest/v1alpha/TopLevel/answerQuery#body.QUERY_PARAMETERS.filter) .

## July 27, 2026

  - add\_circle The Developer Knowledge API now supports the `https://www.googleapis.com/auth/developerprofiles.readonly` OAuth scope.

## July 17, 2026

  - add\_circle The `AnswerQuery` endpoint is now Generally Available (GA). For more information, see [Generate answers from documentation](https://developers.google.com/knowledge/answer-query) .

## July 9, 2026

  - add\_circle The maximum allowed `page_size` for `SearchDocumentChunks` has been increased from 20 to 100.
  - update For `SearchDocumentChunks` , `page_size` values greater than 100 are now coerced to 100 rather than returning an `INVALID_ARGUMENT` error.

## July 2, 2026

  - add\_circle `Document` messages now include a `content_length_bytes` field, which denotes the length of the `content` field in bytes.

## June 9, 2026

  - add\_circle `AnswerQuery` now uses the [`gemini-3-flash-preview`](https://developers.google.com/generative-ai-app-builder/docs/answer-generation-models#models) model.

## June 1, 2026

  - add\_circle [`AnswerQuery`](https://developers.google.com/knowledge/answer-query) responses now include `references` and `citations` for the provided answer.
    
    For more information, see [Generate answers from documentation](https://developers.google.com/knowledge/answer-query) .

## May 20, 2026

  - add\_circle The following domains are now included in the corpus:
    
      - [cloud.google.com](https://cloud.google.com)
      - [dart.dev](https://dart.dev/)
      - [docs.flutter.dev](https://docs.flutter.dev/)
      - [mapsplatform.google.com](https://mapsplatform.google.com)
    
    See the full list of supported domains in the [Corpus Reference](https://developers.google.com/knowledge/reference/corpus-reference) .

## April 20, 2026

  - add\_circle The Developer Knowledge API now supports the `AnswerQuery` method, which lets you generate answers to queries drawn from the [Developer Knowledge API corpus](https://developers.google.com/knowledge/reference/corpus-reference) .
    
    For more information, see [Generate answers from documentation](https://developers.google.com/knowledge/answer-query) .

## April 16, 2026

  - new\_releases The Developer Knowledge API and Developer Knowledge MCP server are now generally available (GA). Use the API and MCP server to give AI-powered development tools the ability to search and retrieve Google's official developer documentation.

## April 14, 2026

  - add\_circle The following domains are now included in the corpus:
    
      - [adk.dev](https://adk.dev)
      - [antigravity.google](http://antigravity.google/)
      - [geminicli.com](https://geminicli.com)
      - [go.dev](https://go.dev)
    
    See the full list of supported domains in the [Corpus Reference](https://developers.google.com/knowledge/reference/corpus-reference) .

## April 9, 2026

  - add\_circle `SearchDocumentChunks` now supports filtering on the Document `data_source` , `update_time` , and `uri` fields. See [Search and retrieve documents](https://developers.google.com/knowledge/howto) and the reference for [`SearchDocumentChunks.filter`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/searchDocumentChunks#body.QUERY_PARAMETERS.filter) for more information.

## April 2, 2026

  - add\_circle `Document` messages now include a `data_source` field, which denotes the source of the content that is being returned.
  - add\_circle The Developer Knowledge API now supports the `DocumentView` enum, allowing you to request document metadata without retrieving the full document content. A `view` field will now be populated on `Document` messages.
  - add\_circle `Document` messages now have an `update_time` field, indicating when the document content or metadata last changed.
  - add\_circle `DocumentChunk` messages now have a `Document` field, containing metadata about the document.

## February 28, 2026

  - add\_circle `Document` messages now include `title` and `description` fields, denoting the title and description of the document.

## March 15, 2026

  - check\_circle Fixed an issue where `Document.uri` values lacked a scheme. They now include a `https://` prefix.

## March 8, 2026

  - update The MCP Tools `get_document` and `batch_get_documents` have been removed. They are replaced by a new `get_documents` MCP Tool.

## February 18, 2026

  - update After March 17, 2026, when you enable the Developer Knowledge API, the Developer Knowledge MCP server is automatically enabled.

## February 4, 2026

  - new\_releases The Developer Knowledge API and Developer Knowledge MCP server are now in Public Preview. Use the API and MCP server to give AI-powered development tools the ability to search and retrieve Google's official developer documentation.
