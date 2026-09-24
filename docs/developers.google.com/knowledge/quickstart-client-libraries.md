---
name: documents/developers.google.com/knowledge/quickstart-client-libraries
uri: https://developers.google.com/knowledge/quickstart-client-libraries
title: 'Quickstart: Use client libraries with the Developer Knowledge API'
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

This guide shows you how to get started with the Developer Knowledge API using official client libraries. You'll learn how to set up your environment, install the client library for your preferred language, and make API calls to search for and retrieve developer documentation.

## Before you begin

Before you start using the Developer Knowledge API client libraries, complete the following sections.

### Enable the API

1.  Open the [Developer Knowledge API page](https://console.cloud.google.com/start/api?id=developerknowledge.googleapis.com) in the Google APIs library.
2.  Check that you have the correct project selected in which you intend to use the API.
3.  Click **Enable** . No specific IAM roles are required to enable or use the API.

### Set up authentication

The Developer Knowledge API client libraries use Application Default Credentials (ADC) to authenticate requests.

To set up local authentication credentials, run the following command:

    gcloud auth application-default login

To learn more about credential options like service accounts, refer to the [Application Default Credentials documentation](https://cloud.google.com/docs/authentication/provide-credentials-adc) .

### Install the client library

To install the official Developer Knowledge API client library, select your programming language:

### Python

    pip install google-developer-knowledge

### Node.js and TypeScript

    npm install @google/developer-knowledge

### Go

    go get cloud.google.com/go/developerknowledge/apiv1

### Java

    <!-- Maven dependency -->
    <dependency>
      <groupId>com.google.cloud</groupId>
      <artifactId>google-cloud-developer-knowledge</artifactId>
      <version>0.3.0</version>
    </dependency>

## Generate answers from documentation

The `AnswerQuery` endpoint answers complex, natural-language questions, such as those involving code setup, troubleshooting procedures, and product capabilities, by pulling information from official documentation sources.

Select a language tab to view an example of how to call `AnswerQuery` :

### Python

``` 
from google.cloud import developer_knowledge_v1


def answer_query(
    query: str = "How do I create a Google Cloud Storage bucket?",
) -> developer_knowledge_v1.AnswerQueryResponse:
    """Answers a developer question grounded in Google developer documentation.

    Args:
        query: The technical question to answer.

    Returns:
        The AnswerQueryResponse containing the grounded answer,
        citations, and references.
    """
    client = developer_knowledge_v1.DeveloperKnowledgeClient()

    request = developer_knowledge_v1.AnswerQueryRequest(
        query=query,
    )

    response = client.answer_query(request=request)

    print(f"Answer:\n{response.answer.answer_text}\n")
    print(f"Citations count: {len(response.answer.citations)}")
    print(f"References count: {len(response.answer.references)}")

    return response

```

### Node.js and TypeScript

    const {DeveloperKnowledgeClient} = require('@google/developer-knowledge');
    
    /**
     * Answers a developer question grounded in Google developer documentation.
     *
     * @param {string} query The technical question to answer.
     */
    async function answerQuery(
      query = 'How do I create a Google Cloud Storage bucket?'
    ) {
      const client = new DeveloperKnowledgeClient();
    
      const request = {
        query,
      };
    
      const [response] = await client.answerQuery(request);
    
      console.log(`Answer:\n${response.answer.answerText}\n`);
      const citationsCount = response.answer.citations
        ? response.answer.citations.length
        : 0;
      const referencesCount = response.answer.references
        ? response.answer.references.length
        : 0;
      console.log(`Citations count: ${citationsCount}`);
      console.log(`References count: ${referencesCount}`);
    
      return response;
    }

### Go

    import (
     "context"
     "fmt"
     "io"
    
     developerknowledge "cloud.google.com/go/developerknowledge/apiv1"
     developerknowledgepb "cloud.google.com/go/developerknowledge/apiv1/developerknowledgepb"
    )
    
    // answerQuery answers a developer question grounded in Google developer documentation.
    func answerQuery(w io.Writer, query string) (*developerknowledgepb.AnswerQueryResponse, error) {
     ctx := context.Background()
    
     client, err := developerknowledge.NewDeveloperKnowledgeClient(ctx)
     if err != nil {
         return nil, fmt.Errorf("developerknowledge.NewDeveloperKnowledgeClient: %w", err)
     }
     defer client.Close()
    
     req := &developerknowledgepb.AnswerQueryRequest{
         Query: query,
     }
    
     resp, err := client.AnswerQuery(ctx, req)
     if err != nil {
         return nil, fmt.Errorf("AnswerQuery: %w", err)
     }
    
     if resp.GetAnswer() != nil {
         fmt.Fprintf(w, "Answer:\n%s\n\n", resp.GetAnswer().GetAnswerText())
         fmt.Fprintf(w, "Citations count: %d\n", len(resp.GetAnswer().GetCitations()))
         fmt.Fprintf(w, "References count: %d\n", len(resp.GetAnswer().GetReferences()))
     }
    
     return resp, nil
    }

### Java

    import com.google.developers.knowledge.v1.AnswerQueryRequest;
    import com.google.developers.knowledge.v1.AnswerQueryResponse;
    import com.google.developers.knowledge.v1.DeveloperKnowledgeClient;
    import java.io.IOException;
    
    public class AnswerQuery {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String query = "How do I create a Google Cloud Storage bucket?";
        answerQuery(query);
      }
    
      // Answers a developer question grounded in Google developer documentation.
      public static AnswerQueryResponse answerQuery(String query) throws IOException {
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DeveloperKnowledgeClient client = DeveloperKnowledgeClient.create()) {
          AnswerQueryRequest request =
              AnswerQueryRequest.newBuilder().setQuery(query).build();
    
          AnswerQueryResponse response = client.answerQuery(request);
    
          System.out.println("Answer:\n" + response.getAnswer().getAnswerText() + "\n");
          System.out.println("Citations count: " + response.getAnswer().getCitationsCount());
          System.out.println("References count: " + response.getAnswer().getReferencesCount());
    
          return response;
        }
      }
    }

## Search for document chunks

To find precise, localized text segments within the documentation rather than a generated answer, use the `SearchDocumentChunks` endpoint. This method scans the corpus and returns individual content snippets (chunks) alongside parent document identifiers, which you can use to retrieve the full document content.

Select a language tab to view an example of how to search document chunks:

### Python

``` 
from google.cloud import developer_knowledge_v1


def search_document_chunks(
    query: str = "How to create a Cloud Storage bucket",
    page_size: int = 5,
) -> (
    developer_knowledge_v1.services.developer_knowledge.pagers.SearchDocumentChunksPager
):
    """Searches developer documentation chunks for a given query.

    Args:
        query: The natural language search query.
        page_size: The maximum number of document chunks to return.

    Returns:
        The SearchDocumentChunksPager containing relevant document chunks.
    """
    client = developer_knowledge_v1.DeveloperKnowledgeClient()

    request = developer_knowledge_v1.SearchDocumentChunksRequest(
        query=query,
        page_size=page_size,
    )

    response = client.search_document_chunks(request=request)

    count = 0
    for chunk in response:
        print(f"Parent Document: {chunk.parent}")
        print(f"Chunk ID: {chunk.id}")
        print(f"Content: {chunk.content[:100]}...\n")
        count += 1
        if page_size > 0 and count >= page_size:
            break

    return response

```

### Node.js and TypeScript

    const {DeveloperKnowledgeClient} = require('@google/developer-knowledge');
    
    /**
     * Searches developer documentation chunks for a given query.
     *
     * @param {string} query The search query string.
     * @param {number} pageSize The maximum number of document chunks to return.
     */
    async function searchDocumentChunks(
      query = 'How to create a Cloud Storage bucket',
      pageSize = 5
    ) {
      const client = new DeveloperKnowledgeClient();
    
      const request = {
        query,
        pageSize,
      };
    
      // Warning: Should always disable autoPaginate to avoid iterating through all pages.
      // By default NodeJS SDK returns an iterable where you can iterate through all
      // search results instead of only the limited number of results requested on pageSize.
      const [chunks] = await client.searchDocumentChunks(request, {
        autoPaginate: false,
      });
    
      for (const chunk of chunks) {
        console.log(`Parent Document: ${chunk.parent}`);
        console.log(`Chunk ID: ${chunk.id}`);
        console.log(`Content Preview: ${chunk.content.substring(0, 100)}...\n`);
      }
    
      return chunks;
    }

### Go

    import (
     "context"
     "fmt"
     "io"
    
     developerknowledge "cloud.google.com/go/developerknowledge/apiv1"
     developerknowledgepb "cloud.google.com/go/developerknowledge/apiv1/developerknowledgepb"
     "google.golang.org/api/iterator"
    )
    
    // searchDocumentChunks searches developer documentation chunks for a given query.
    func searchDocumentChunks(w io.Writer, query string, pageSize int32) ([]*developerknowledgepb.DocumentChunk, error) {
     ctx := context.Background()
    
     client, err := developerknowledge.NewDeveloperKnowledgeClient(ctx)
     if err != nil {
         return nil, fmt.Errorf("developerknowledge.NewDeveloperKnowledgeClient: %w", err)
     }
     defer client.Close()
    
     req := &developerknowledgepb.SearchDocumentChunksRequest{
         Query:    query,
         PageSize: pageSize,
     }
    
     var results []*developerknowledgepb.DocumentChunk
     it := client.SearchDocumentChunks(ctx, req)
     for {
         chunk, err := it.Next()
         if err == iterator.Done {
             break
         }
         if err != nil {
             return nil, fmt.Errorf("SearchDocumentChunks: %w", err)
         }
         results = append(results, chunk)
         fmt.Fprintf(w, "Parent Document: %s\n", chunk.GetParent())
         fmt.Fprintf(w, "Chunk ID: %s\n", chunk.GetId())
         fmt.Fprintf(w, "Content: %s\n\n", chunk.GetContent())
    
         if pageSize > 0 && len(results) >= int(pageSize) {
             break
         }
     }
    
     return results, nil
    }

### Java

    import com.google.developers.knowledge.v1.DeveloperKnowledgeClient;
    import com.google.developers.knowledge.v1.DeveloperKnowledgeClient.SearchDocumentChunksPagedResponse;
    import com.google.developers.knowledge.v1.DocumentChunk;
    import com.google.developers.knowledge.v1.SearchDocumentChunksRequest;
    import java.io.IOException;
    
    public class SearchDocumentChunks {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String query = "How to create a Cloud Storage bucket";
        int pageSize = 5;
        searchDocumentChunks(query, pageSize);
      }
    
      // Searches developer documentation chunks for a given query.
      public static SearchDocumentChunksPagedResponse searchDocumentChunks(
          String query, int pageSize) throws IOException {
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DeveloperKnowledgeClient client = DeveloperKnowledgeClient.create()) {
          SearchDocumentChunksRequest request =
              SearchDocumentChunksRequest.newBuilder()
                  .setQuery(query)
                  .setPageSize(pageSize)
                  .build();
    
          SearchDocumentChunksPagedResponse response = client.searchDocumentChunks(request);
    
          for (DocumentChunk chunk : response.getPage().getValues()) {
            System.out.println("Parent Document: " + chunk.getParent());
            System.out.println("Chunk ID: " + chunk.getId());
            String preview = chunk.getContent();
            if (preview.length() > 100) {
              preview = preview.substring(0, 100) + "...";
            }
            System.out.println("Content: " + preview + "\n");
          }
    
          return response;
        }
      }
    }

## Retrieve a document

Each document chunk contains a `parent` field with the resource name of its parent document. Use `GetDocument` with that resource name to retrieve the full document.

The following samples retrieve a sample document. You can replace the sample document name with any `parent` resource name returned from your search results.

Select a language tab to view an example of how to call `GetDocument` :

### Python

``` 
from google.cloud import developer_knowledge_v1


def get_document(
    name: str = "documents/docs.cloud.google.com/storage/docs/creating-buckets",
) -> developer_knowledge_v1.Document:
    """Retrieves a single developer documentation page by its resource name.

    Args:
        name: The resource name of the document in format
            'documents/{uri_without_scheme}'.

    Returns:
        The Document containing the full Markdown content and metadata.
    """
    client = developer_knowledge_v1.DeveloperKnowledgeClient()

    request = developer_knowledge_v1.GetDocumentRequest(
        name=name,
    )

    document = client.get_document(request=request)

    print(f"Title: {document.title}")
    print(f"URI: {document.uri}")
    print(f"Data Source: {document.data_source}")
    print(f"Content Length: {document.content_length_bytes} bytes")
    print(f"Content Preview: {document.content[:150]}...\n")

    return document

```

### Node.js and TypeScript

    const {DeveloperKnowledgeClient} = require('@google/developer-knowledge');
    
    /**
     * Retrieves a single developer documentation page by its resource name.
     *
     * @param {string} name The resource name in format 'documents/{uri_without_scheme}'.
     */
    async function getDocument(
      name = 'documents/docs.cloud.google.com/storage/docs/creating-buckets'
    ) {
      const client = new DeveloperKnowledgeClient();
    
      const request = {
        name,
      };
    
      const [document] = await client.getDocument(request);
    
      console.log(`Title: ${document.title}`);
      console.log(`URI: ${document.uri}`);
      console.log(`Data Source: ${document.dataSource}`);
      console.log(`Content Length: ${document.contentLengthBytes} bytes`);
      console.log(`Content Preview: ${document.content.substring(0, 150)}...\n`);
    
      return document;
    }

### Go

    import (
     "context"
     "fmt"
     "io"
    
     developerknowledge "cloud.google.com/go/developerknowledge/apiv1"
     developerknowledgepb "cloud.google.com/go/developerknowledge/apiv1/developerknowledgepb"
    )
    
    // getDocument retrieves a single developer documentation page by its resource name.
    func getDocument(w io.Writer, name string) (*developerknowledgepb.Document, error) {
     ctx := context.Background()
    
     client, err := developerknowledge.NewDeveloperKnowledgeClient(ctx)
     if err != nil {
         return nil, fmt.Errorf("developerknowledge.NewDeveloperKnowledgeClient: %w", err)
     }
     defer client.Close()
    
     req := &developerknowledgepb.GetDocumentRequest{
         Name: name,
     }
    
     doc, err := client.GetDocument(ctx, req)
     if err != nil {
         return nil, fmt.Errorf("GetDocument: %w", err)
     }
    
     fmt.Fprintf(w, "Title: %s\n", doc.GetTitle())
     fmt.Fprintf(w, "URI: %s\n", doc.GetUri())
     fmt.Fprintf(w, "Data Source: %s\n", doc.GetDataSource())
     fmt.Fprintf(w, "Content Length: %d bytes\n\n", doc.GetContentLengthBytes())
    
     return doc, nil
    }

### Java

    import com.google.developers.knowledge.v1.DeveloperKnowledgeClient;
    import com.google.developers.knowledge.v1.Document;
    import com.google.developers.knowledge.v1.GetDocumentRequest;
    import java.io.IOException;
    
    public class GetDocument {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String name = "documents/docs.cloud.google.com/storage/docs/creating-buckets";
        getDocument(name);
      }
    
      // Retrieves a single developer documentation page by its resource name.
      public static Document getDocument(String name) throws IOException {
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DeveloperKnowledgeClient client = DeveloperKnowledgeClient.create()) {
          GetDocumentRequest request = GetDocumentRequest.newBuilder().setName(name).build();
    
          Document document = client.getDocument(request);
    
          System.out.println("Title: " + document.getTitle());
          System.out.println("URI: " + document.getUri());
          System.out.println("Data Source: " + document.getDataSource());
          System.out.println("Content Length: " + document.getContentLengthBytes() + " bytes");
          String preview = document.getContent();
          if (preview.length() > 150) {
            preview = preview.substring(0, 150) + "...";
          }
          System.out.println("Content Preview: " + preview + "\n");
    
          return document;
        }
      }
    }

## Retrieve multiple documents

Use `BatchGetDocuments` to retrieve up to 20 documents by resource name in a single API call.

Select a language tab to view an example of how to call `BatchGetDocuments` :

### Python

``` 
from typing import List, Optional

from google.cloud import developer_knowledge_v1


def batch_get_documents(
    names: Optional[List[str]] = None,
) -> developer_knowledge_v1.BatchGetDocumentsResponse:
    """Retrieves multiple developer documentation pages in a single request.

    Args:
        names: A list of resource names in format 'documents/{uri_without_scheme}'.

    Returns:
        The BatchGetDocumentsResponse containing the retrieved documents.
    """
    if names is None:
        names = [
            "documents/docs.cloud.google.com/storage/docs/creating-buckets",
            "documents/docs.cloud.google.com/storage/docs/deleting-buckets",
        ]

    client = developer_knowledge_v1.DeveloperKnowledgeClient()

    request = developer_knowledge_v1.BatchGetDocumentsRequest(
        names=names,
    )

    response = client.batch_get_documents(request=request)

    for doc in response.documents:
        print(f"Title: {doc.title}")
        print(f"URI: {doc.uri}")
        print(f"Content Length: {doc.content_length_bytes} bytes\n")

    return response

```

### Node.js and TypeScript

    const {DeveloperKnowledgeClient} = require('@google/developer-knowledge');
    
    /**
     * Retrieves multiple developer documentation pages in a single request.
     *
     * @param {string[]} names Array of resource names in format 'documents/{uri_without_scheme}'.
     */
    async function batchGetDocuments(
      names = [
        'documents/docs.cloud.google.com/storage/docs/creating-buckets',
        'documents/docs.cloud.google.com/storage/docs/deleting-buckets',
      ]
    ) {
      const client = new DeveloperKnowledgeClient();
    
      const request = {
        names,
      };
    
      const [response] = await client.batchGetDocuments(request);
    
      if (response.documents) {
        for (const doc of response.documents) {
          console.log(`Title: ${doc.title}`);
          console.log(`URI: ${doc.uri}`);
          console.log(`Content Length: ${doc.contentLengthBytes} bytes\n`);
        }
      }
    
      return response;
    }

### Go

    import (
     "context"
     "fmt"
     "io"
    
     developerknowledge "cloud.google.com/go/developerknowledge/apiv1"
     developerknowledgepb "cloud.google.com/go/developerknowledge/apiv1/developerknowledgepb"
    )
    
    // batchGetDocuments retrieves multiple developer documentation pages in a single request.
    func batchGetDocuments(w io.Writer, names []string) (*developerknowledgepb.BatchGetDocumentsResponse, error) {
     ctx := context.Background()
    
     client, err := developerknowledge.NewDeveloperKnowledgeClient(ctx)
     if err != nil {
         return nil, fmt.Errorf("developerknowledge.NewDeveloperKnowledgeClient: %w", err)
     }
     defer client.Close()
    
     req := &developerknowledgepb.BatchGetDocumentsRequest{
         Names: names,
     }
    
     resp, err := client.BatchGetDocuments(ctx, req)
     if err != nil {
         return nil, fmt.Errorf("BatchGetDocuments: %w", err)
     }
    
     for _, doc := range resp.GetDocuments() {
         fmt.Fprintf(w, "Title: %s\n", doc.GetTitle())
         fmt.Fprintf(w, "\tURI: %s\n", doc.GetUri())
         fmt.Fprintf(w, "\tContent Length: %d bytes\n\n", doc.GetContentLengthBytes())
     }
    
     return resp, nil
    }

### Java

    import com.google.developers.knowledge.v1.BatchGetDocumentsRequest;
    import com.google.developers.knowledge.v1.BatchGetDocumentsResponse;
    import com.google.developers.knowledge.v1.DeveloperKnowledgeClient;
    import com.google.developers.knowledge.v1.Document;
    import java.io.IOException;
    import java.util.Arrays;
    import java.util.List;
    
    public class BatchGetDocuments {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        List<String> names =
            Arrays.asList(
                "documents/docs.cloud.google.com/storage/docs/creating-buckets",
                "documents/docs.cloud.google.com/storage/docs/deleting-buckets");
        batchGetDocuments(names);
      }
    
      // Retrieves multiple developer documentation pages in a single request.
      public static BatchGetDocumentsResponse batchGetDocuments(List<String> names) throws IOException {
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DeveloperKnowledgeClient client = DeveloperKnowledgeClient.create()) {
          BatchGetDocumentsRequest request =
              BatchGetDocumentsRequest.newBuilder().addAllNames(names).build();
    
          BatchGetDocumentsResponse response = client.batchGetDocuments(request);
    
          for (Document doc : response.getDocumentsList()) {
            System.out.println("Title: " + doc.getTitle());
            System.out.println("URI: " + doc.getUri());
            System.out.println("Content Length: " + doc.getContentLengthBytes() + " bytes\n");
          }
    
          return response;
        }
      }
    }

## What's next

  - Explore the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) to view the full list of included documentation.
  - Refer to the [API reference documentation](https://developers.google.com/knowledge/reference/rest) for details on API methods and parameters.
  - Learn how to [set up the MCP server in Google Antigravity](https://codelabs.developers.google.com/developer-knowledge-mcp-antigravity) .
