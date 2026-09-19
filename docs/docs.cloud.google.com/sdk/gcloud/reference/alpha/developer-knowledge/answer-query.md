---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/answer-query
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/answer-query
title: gcloud alpha developer-knowledge answer-query
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha developer-knowledge answer-query - answer a natural language query using grounded generation

SYNOPSIS

`gcloud alpha developer-knowledge answer-query` `  --query  ` = `  QUERY  ` \[ `  --query-filter  ` = `  QUERY_FILTER  ` \] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Answer a natural language query using grounded generation based on the Developer Knowledge corpus.

EXAMPLES

To answer a question using grounded generation:

    gcloud alpha developer-knowledge answer-query --query="What is the difference between a global and regional load balancer?"

To answer a question with corpus filtering:

    gcloud alpha developer-knowledge answer-query --query="How do I deploy a Cloud Run function?" --query-filter='data_source = "docs.cloud.google.com"'

REQUIRED FLAGS

  - `--query` = `  QUERY  `  
    The query to answer.

OPTIONAL FLAGS

  - `--query-filter` = `  QUERY_FILTER  `  
    Apply a strict filter to the search results used to ground the answer. Supported filter fields: `content_length_bytes` , `data_source` , `update_time` , `uri` . Example: `data_source = "docs.cloud.google.com"` .

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

API REFERENCE

This command uses the `developerknowledge/v1alpha` API. The full documentation for this API can be found at: <https://developers.google.com/knowledge>

GUIDANCE

Use `answer-query` to get synthesized natural language answers with source citations.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. This variant is also available:

    gcloud beta developer-knowledge answer-query
