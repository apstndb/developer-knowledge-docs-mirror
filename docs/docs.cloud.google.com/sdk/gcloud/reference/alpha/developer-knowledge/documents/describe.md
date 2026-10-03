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

`gcloud alpha developer-knowledge documents describe` [`NAME`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe#NAME) \[ [`--view`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe#--view) = `VIEW` ; default="content"\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/developer-knowledge/documents/describe#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Retrieve a single document and metadata based on its resource name/URI.

EXAMPLES

To retrieve the full Markdown content along with the metadata of a document, run:

```
gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets
```

To retrieve only the basic metadata (like title and data source) of a specific document, run:

```
gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets --view=basic
```

To retrieve the complete document record, including all available backend fields, metadata, and full Markdown content, run:

```
gcloud alpha developer-knowledge documents describe documents/docs.cloud.google.com/storage/docs/creating-buckets --view=full
```

POSITIONAL ARGUMENTS

`NAME`  
The resource name of the document to retrieve. Format: `documents/{uri_without_scheme}` (e.g., `documents/docs.cloud.google.com/storage/docs/creating-buckets` ).

FLAGS

`--view` = `VIEW` ; default="content"  
Specify which fields of the document are included in the response. `VIEW` must be one of:

`basic`  
Include basic metadata fields (e.g., URI, data source, title).

`content`  
Include basic fields and the Markdown content.

`full`  
Include all document fields.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `developerknowledge/v1alpha` API. The full documentation for this API can be found at: <https://developers.google.com/knowledge>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

```
gcloud developer-knowledge documents describe
```

```
gcloud beta developer-knowledge documents describe
```
