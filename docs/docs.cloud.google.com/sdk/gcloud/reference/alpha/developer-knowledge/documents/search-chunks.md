---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/search-chunks
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/search-chunks
title: gcloud alpha developer-knowledge documents search-chunks
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha developer-knowledge documents search-chunks - search for developer knowledge across Google's developer documentation

SYNOPSIS

`gcloud alpha developer-knowledge documents search-chunks` `  --query  ` = `  QUERY  ` \[ `  --query-filter  ` = `  QUERY_FILTER  ` \] \[ `  --filter  ` = `  EXPRESSION  ` \] \[ `  --limit  ` = `  LIMIT  ` ; default=5\] \[ `  --page-size  ` = `  PAGE_SIZE  ` \] \[ `  --sort-by  ` =\[ `  FIELD  ` , …\]\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Search for developer knowledge across Google's developer documentation. Return DocumentChunks based on the user's query.

There may be many chunks from the same Document. To retrieve full documents, use `  gcloud alpha developer-knowledge documents describe  ` with the DocumentChunk.parent returned in the search-chunks results.

EXAMPLES

To search for document chunks answering a query:

    gcloud alpha developer-knowledge documents search-chunks --query="How to create a Cloud Storage bucket?"

To search for document chunks filtered by data source:

    gcloud alpha developer-knowledge documents search-chunks --query="Cloud Functions deployment" --query-filter='data_source = "docs.cloud.google.com"'

To search with custom pagination:

    gcloud alpha developer-knowledge documents search-chunks --query="Compute Engine instances" --page-size=10 --limit=20

REQUIRED FLAGS

  - `--query` = `  QUERY  `  
    Raw query string provided by the user, such as "How to create a Cloud Storage bucket?".

FLAGS

  - `--query-filter` = `  QUERY_FILTER  `  
    Apply a strict filter to the search results. Supported filter fields: `data_source` , `update_time` , `uri` . Example: `data_source = "docs.cloud.google.com"` .

LIST COMMAND FLAGS

  - `--filter` = `  EXPRESSION  `  
    Apply a Boolean filter `  EXPRESSION  ` to each resource item to be listed. If the expression evaluates `True` , then that item is listed. For more details and examples of filter expressions, run $ [gcloud topic filters](https://docs.cloud.google.com/sdk/gcloud/reference/topic/filters) . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .
  - `--limit` = `  LIMIT  ` ; default=5  
    Maximum number of resources to list. The default is `5` . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .
  - `--page-size` = `  PAGE_SIZE  `  
    Some services group resource list output into pages. This flag specifies the maximum number of resources per page. The default is determined by the service if it supports paging, otherwise it is `unlimited` (no paging). Paging may be applied before or after `--filter` and `--limit` depending on the service.
  - `--sort-by` =\[ `  FIELD  ` ,…\]  
    Comma-separated list of resource field key names to sort by. The default order is ascending. Prefix a field with \`\`\~´´ for descending order on that field. This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

API REFERENCE

This command uses the developerknowledge API. The full documentation for this API can be found at: <https://developers.google.com/knowledge>

GUIDANCE

When searching for information, use `search-chunks` first to discover relevant document chunks, and then use `describe` on the chunk's parent to retrieve the full document if necessary.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

    gcloud developer-knowledge documents search-chunks

    gcloud beta developer-knowledge documents search-chunks
