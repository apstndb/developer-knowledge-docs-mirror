---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe
title: gcloud alpha developer-knowledge documents describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha developer-knowledge documents describe - retrieve a single document with its full Markdown content

SYNOPSIS

`gcloud alpha developer-knowledge documents describe` `  NAME  ` \[ `  --view  ` = `  VIEW  ` ; default="content"\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Retrieve a single document and metadata based on its resource name/URI.

EXAMPLES

To retrieve the full Markdown content along with the metadata of a document, run:

    gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets

To retrieve only the basic metadata (like title and data source) of a specific document, run:

    gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets --view=basic

To retrieve the complete document record, including all available backend fields, metadata, and full Markdown content, run:

    gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets --view=full

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The resource name of the document to retrieve. Format: `documents/{uri_without_scheme}` (e.g., `documents/docs.cloud.google.com/storage/docs/creating-buckets` ).

FLAGS

  - `--view` = `  VIEW  ` ; default="content"  
    Specify which fields of the document are included in the response. `  VIEW  ` must be one of:
      - `basic`  
        Include basic metadata fields (e.g., URI, data source, title).
      - `content`  
        Include basic fields and the Markdown content.
      - `full`  
        Include all document fields.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

API REFERENCE

This command uses the `developerknowledge/v1alpha` API. The full documentation for this API can be found at: <https://developers.google.com/knowledge>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. This variant is also available:

    gcloud beta developer-knowledge documents describe
