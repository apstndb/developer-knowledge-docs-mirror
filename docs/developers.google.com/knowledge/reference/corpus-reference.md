---
name: documents/developers.google.com/knowledge/reference/corpus-reference
uri: https://developers.google.com/knowledge/reference/corpus-reference
title: Corpus reference
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The Developer Knowledge API and MCP server can search and get documents from public pages in the following domains:

  - [adk.dev](https://adk.dev)

  - [ai.google.dev](http://ai.google.dev/)

  - [antigravity.google](http://antigravity.google/)

  - [cloud.google.com](https://cloud.google.com)

  - [dart.dev](https://dart.dev/)

  - [developer.android.com](http://developer.android.com)

  - [developer.chrome.com](http://developer.chrome.com)

  - [developers.home.google.com](http://developers.home.google.com)

  - [developers.google.com](http://developers.google.com)

  - [docs.apigee.com](https://docs.apigee.com/)

  - [docs.cloud.google.com](http://docs.cloud.google.com)
    
    Exceptions
    
    Pages with the following prefixes are not included in the corpus:
    
      - docs.cloud.google.com/cpp/docs/reference
      - docs.cloud.google.com/dotnet/docs/reference
      - docs.cloud.google.com/go/docs/reference
      - docs.cloud.google.com/java/docs/reference
      - docs.cloud.google.com/nodejs/docs/reference
      - docs.cloud.google.com/php/docs/reference
      - docs.cloud.google.com/python/docs/reference
      - docs.cloud.google.com/ruby/docs/reference
      - docs.cloud.google.com/rust/docs/reference

  - [docs.flutter.dev](https://docs.flutter.dev/)

  - [firebase.google.com](http://firebase.google.com)

  - [fuchsia.dev](https://fuchsia.dev/)

  - [geminicli.com](https://geminicli.com)

  - [genkit.dev](https://genkit.dev/)

  - [go.dev](https://go.dev)

  - [mapsplatform.google.com](https://mapsplatform.google.com)

  - [web.dev](https://web.dev)

  - [www.tensorflow.org](http://www.tensorflow.org)

## Filter examples

To restrict search results to specific domains, use the `filter` parameter when calling [`SearchDocumentChunks`](https://developers.google.com/knowledge/reference/rest/v1alpha/documents/searchDocumentChunks) :

  - **Single data source** :
    
        data_source = "docs.cloud.google.com"

  - **Multiple data sources** :
    
        data_source = "docs.cloud.google.com" OR data_source = "firebase.google.com"

## Data freshness

The Developer Knowledge API aims to provide access to the latest Google developer documentation. Our goal is to re-index content within 48 hours of publication so that new or updated documentation is available within 2 business days.
