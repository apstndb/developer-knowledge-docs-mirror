---
name: documents/developers.google.com/knowledge/client-libraries
uri: https://developers.google.com/knowledge/client-libraries
title: Developer Knowledge API client libraries
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

This page shows how to get started with the Cloud Client Libraries for the Developer Knowledge API. Instead of constructing raw HTTP requests, client libraries provide idiomatic types, built-in authentication, automatic pagination, and retry handling that reduce the amount of code you need to write.

To learn more about client libraries for Google APIs, refer to [Client libraries explained](https://cloud.google.com/apis/docs/client-libraries-explained) .

> **Tip:** To view complete Go, Java, Node.js, and Python code samples for searching documentation chunks, retrieving documents, and generating grounded answers, check out [Quickstart: Use client libraries with the Developer Knowledge API](https://developers.google.com/knowledge/quickstart-client-libraries) .

## Install the client library

Select your programming language to install the official Developer Knowledge API client library:

### Go

Add the module to your Go project:

```
go get cloud.google.com/go/developerknowledge/apiv1
```

To learn more, refer to [Setting up a Go development environment](https://cloud.google.com/go/docs/setup) .

### Java

If you use Maven, add the following dependency to your `pom.xml` file:

```
<dependency>
  <groupId>com.google.cloud</groupId>
  <artifactId>google-cloud-developer-knowledge</artifactId>
  <version>0.6.0</version>
</dependency>
```

If you use Gradle, add the following dependency to your `build.gradle` file:

```
implementation 'com.google.cloud:google-cloud-developer-knowledge:0.6.0'
```

To learn more, refer to [Setting up a Java development environment](https://cloud.google.com/java/docs/setup) .

### Node.js and TypeScript

Install the package using `npm` :

```
npm install @google/developer-knowledge
```

To learn more, refer to [Setting up a Node.js development environment](https://cloud.google.com/nodejs/docs/setup) .

### PHP

Install the package using Composer:

```
composer require google/developer-knowledge
```

To learn more, refer to [Using PHP on Google Cloud](https://cloud.google.com/php/docs) .

### Python

Install the package using `pip` :

```
pip install --upgrade google-developer-knowledge
```

To learn more, refer to [Setting up a Python development environment](https://cloud.google.com/python/docs/setup) .

### Ruby

Install the gem:

```
gem install google-developers-developer_knowledge
```

To learn more, refer to [Setting up a Ruby development environment](https://cloud.google.com/ruby/docs/setup) .

## Set up authentication

Before making API requests, make sure that you have [enabled the Developer Knowledge API](https://developers.google.com/knowledge/quickstart-client-libraries#enable-api) in your Google Cloud project.

To authenticate calls to the Developer Knowledge API, client libraries support [Application Default Credentials (ADC)](https://cloud.google.com/docs/authentication/application-default-credentials) . The libraries look for credentials in a set of defined locations and use those credentials to authenticate requests to the API. With ADC, you can make credentials available to your application in a variety of environments, such as local development or production, without needing to modify your application code.

For production environments, the way you set up ADC depends on the service and context:

- **Google Cloud environments** : when your application runs on Cloud Run, Google Kubernetes Engine, Compute Engine, or Cloud Run functions, ADC automatically uses the service account attached to the compute resource.
- **External or on-premises environments** : use [Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation) or set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to the path of a credential configuration file.

To learn more about production credential options, refer to [Set up Application Default Credentials](https://cloud.google.com/docs/authentication/provide-credentials-adc) .

For a local development environment, you can set up ADC with the credentials associated with your Google Account:

1.  [Install](https://cloud.google.com/sdk/docs/install) and [initialize](https://cloud.google.com/sdk/docs/initializing) the gcloud CLI.

2.  Create local authentication credentials for your Google Account:

    ```
    gcloud auth application-default login
    ```

    A sign-in screen appears. After you sign in, your credentials are stored in the local credential file used by ADC.

## Additional resources

Select a language tab to find links to API reference documentation, code samples, best practices, issue trackers, and source code repositories for each client library:

### Go

The following list contains links to more resources related to the client library for Go:

- [API reference](https://developers.google.com/go/docs/reference/cloud.google.com/go/developerknowledge/latest)
- [Package on pkg.go.dev](https://pkg.go.dev/cloud.google.com/go/developerknowledge/apiv1)
- [Code samples on GitHub](https://github.com/GoogleCloudPlatform/golang-samples/tree/main/developerknowledge)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
- [Source code](https://github.com/googleapis/google-cloud-go/tree/main/developerknowledge)

### Java

The following list contains links to more resources related to the client library for Java:

- [API reference](https://developers.google.com/java/docs/reference/google-cloud-developer-knowledge/latest)
- [Artifact on Maven Central](https://central.sonatype.com/artifact/com.google.cloud/google-cloud-developer-knowledge)
- [Code samples on GitHub](https://github.com/GoogleCloudPlatform/java-docs-samples/tree/main/developer-knowledge)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-java/issues)
- [Source code](https://github.com/googleapis/google-cloud-java/tree/main/java-developerknowledge)

### Node.js and TypeScript

The following list contains links to more resources related to the client library for Node.js and TypeScript:

- [Package on npm](https://www.npmjs.com/package/@google/developer-knowledge)
- [Code samples on GitHub](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/tree/main/developer-knowledge)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-node/issues)
- [Source code](https://github.com/googleapis/google-cloud-node/tree/main/packages/google-developer-knowledge)

### PHP

The following list contains links to more resources related to the client library for PHP:

- [API reference](https://developers.google.com/php/docs/reference/developer-knowledge/latest)
- [Package on Packagist](https://packagist.org/packages/google/developer-knowledge)
- [Code samples on GitHub](https://github.com/googleapis/google-cloud-php/tree/main/DeveloperKnowledge/samples/V1/DeveloperKnowledgeClient)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
- [Source code](https://github.com/googleapis/google-cloud-php/tree/main/DeveloperKnowledge)

### Python

The following list contains links to more resources related to the client library for Python:

- [API reference](https://developers.google.com/python/docs/reference/google-developer-knowledge/latest)
- [Package on PyPI](https://pypi.org/project/google-developer-knowledge/)
- [Code samples on GitHub](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/developer-knowledge)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-python/issues)
- [Source code](https://github.com/googleapis/google-cloud-python/tree/main/packages/google-developer-knowledge)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

- [API reference](https://developers.google.com/ruby/docs/reference/google-developers-developer_knowledge-v1/latest)
- [Gem on RubyGems](https://rubygems.org/gems/google-developers-developer_knowledge)
- [Code samples on GitHub](https://github.com/googleapis/google-cloud-ruby/tree/main/google-developers-developer_knowledge-v1/snippets/developer_knowledge)
- [Client libraries best practices](https://cloud.google.com/apis/docs/client-libraries-best-practices)
- [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
- [Source code](https://github.com/googleapis/google-cloud-ruby/tree/main/google-developers-developer_knowledge)

## What's next

- Follow the [client libraries quickstart](https://developers.google.com/knowledge/quickstart-client-libraries) to view and run code samples for `AnswerQuery` , `SearchDocumentChunks` , `GetDocument` , and `BatchGetDocuments` .
- Learn more about query filters, pagination, and field masks in [Search and retrieve documents](https://developers.google.com/knowledge/howto) .
- Use grounded generation with [Generate answers from documentation](https://developers.google.com/knowledge/answer-query) .
- Review retry strategies and status codes in [Error handling, rate limiting, and quota management](https://developers.google.com/knowledge/error-handling-and-limits) .
- Browse the [corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) to view all supported documentation domains.
