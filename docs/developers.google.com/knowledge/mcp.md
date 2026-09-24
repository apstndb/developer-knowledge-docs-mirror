---
name: documents/developers.google.com/knowledge/mcp
uri: https://developers.google.com/knowledge/mcp
title: Connect to the Developer Knowledge MCP server
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

The Google Developer Knowledge MCP server gives AI-powered development tools direct access to search and retrieve official Google developer documentation for products like Firebase, Google Cloud, Android, Google Maps Platform, and more. By connecting your coding assistant to Google's authoritative library of documentation, you avoid manual web searches, outdated context, and scraping.

## MCP server capabilities

The Google Developer Knowledge MCP server provides three core tools to your AI coding assistant:

| Tool name          | Description                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------- |
| `search_documents` | Searches Google developer documentation and returns the most relevant page excerpts alongside their document names. |
| `get_documents`    | Retrieves the full Markdown content of documents using the names returned by `search_documents` .                   |
| `answer_query`     | Generates structured answers drawn from the Developer Knowledge corpus.                                             |

The `search_documents` tool searches Google's documentation to find the most relevant sections matching your query. When you ask a question, the tool returns short text passages. If your agent needs the complete page context surrounding a passage, it can pass the document's resource name to `get_documents` to retrieve the entire page.

Use the `answer_query` tool when you want a direct answer to a question drawn from the [Developer Knowledge corpus](https://developers.google.com/knowledge/reference/corpus-reference) rather than raw search results or full Markdown files.

## Choose your authentication method

The Developer Knowledge MCP server supports two authentication methods depending on your development environment and AI assistant:

  - **API key** : Best for third-party IDEs and CLI agents such as Claude Code, Cursor, GitHub Copilot, Codex, and other remote MCP clients. Pass the API key in the `X-Goog-Api-Key` header over HTTPS.
  - **OAuth and ADC** : Best for Google Antigravity or enterprise workflows that use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) or a standalone OAuth 2.0 Client ID.

Generate the credentials required for your chosen authentication method to allow your AI assistant or coding agent to authenticate requests with the Developer Knowledge MCP server service.

Select a tab to create your credentials:

### API key

#### Prerequisites

Before creating an API key, ensure you have:

  - [A Google Cloud project](https://developers.google.com/workspace/guides/create-project) .
  - [The gcloud CLI installed](https://cloud.google.com/sdk/docs/install) (if configuring from the command line).

#### Enable the API and create an API key

You can generate an API key using either the Google Cloud console or the gcloud CLI:

### Google Cloud Console

1.  Open the [Developer Knowledge API page](https://console.cloud.google.com/start/api?id=developerknowledge.googleapis.com) in the Google Cloud console.
2.  Select your Google Cloud project and click **Enable** .
3.  Go to the [Credentials page](https://console.cloud.google.com/apis/credentials) .
4.  Click **Create credentials** and select **API key** .
5.  Click the **Edit API key** action to configure restrictions:
      - Under **API restrictions** , choose **Restrict key** .
      - Select **Developer Knowledge API** .
      - If you plan to use this same key for model calls (such as `GEMINI_API_KEY` ), also select **Generative Language API** .
6.  Click **Save** , then copy your API key.

### gcloud CLI

1.  Enable the Developer Knowledge API in your project, replacing PROJECT\_ID with your project ID:
    
        gcloud services enable developerknowledge.googleapis.com \
          --project=PROJECT_ID

2.  Create an API key:
    
        gcloud services api-keys create \
          --project=PROJECT_ID \
          --display-name="DK API Key"
    
    This command returns metadata details about your new key. Copy and save both of the following values from the command output:
    
      - `keyString` : this is the raw API key (for example, `AIzaSy...` ). You will paste this value into your IDE configuration.
      - `name` : this is the key's resource path (for example, `projects/PROJECT_ID/locations/global/keys/UNIQUE_ID` ). You will use this path to restrict the key in the next step.

3.  Restrict the key to the Developer Knowledge API to help prevent unauthorized use. Replace KEY\_NAME with the full `name` path copied from the previous step:
    
        gcloud services api-keys update KEY_NAME \
          --api-target=service=developerknowledge.googleapis.com
    
    > **Important:** If you plan to use this same key for your AI client's general model calls (for example, `GEMINI_API_KEY` ), you must also allow the Generative Language API:
    
        gcloud services api-keys update KEY_NAME \
          --api-target=service=developerknowledge.googleapis.com \
          --api-target=service=generativelanguage.googleapis.com

### OAuth and ADC

#### Prerequisites

Before configuring OAuth, make sure you have:

  - [A Google Cloud project](https://developers.google.com/workspace/guides/create-project) .
  - [The gcloud CLI installed](https://cloud.google.com/sdk/docs/install) .

#### Enable the API

Run the following command to enable the Developer Knowledge API in your project:

    gcloud services enable developerknowledge.googleapis.com \
      --project=PROJECT_ID

#### Choose your OAuth credential type

Select the credential approach required by your tool:

### Application Default Credentials

If your AI assistant supports ADC (such as Google Antigravity):

1.  Authenticate with your Google Account and set your quota project:
    
        gcloud auth application-default login \
          --project=PROJECT_ID

2.  When your browser opens, sign in with your Google Account and grant the requested permissions.

### OAuth client ID

If your AI assistant requires a standalone OAuth client ID and secret:

1.  Open the [OAuth consent screen](https://console.cloud.google.com/auth/overview?project=_) .
2.  Set the user type to **External** , fill in the required app name and support email, and click **Save and continue** .
3.  On the [Audience page](https://console.cloud.google.com/auth/audience?project=_) , click **Add users** under **Test users** , enter your Google email address, and click **Save** .
4.  Go to the [Clients page](https://console.cloud.google.com/auth/clients?project=_) , click **Create client** , and set **Application type** to **Desktop app** .
5.  Click **Create** , then download the JSON client credentials file.

## Configure your IDE or coding agent

After obtaining your credentials, select your preferred coding environment to view setup instructions.

Depending on your chosen authentication method, replace the placeholders in the configuration templates as follows:

  - **API key authentication** : Replace YOUR\_API\_KEY with your raw API key string.

  - **OAuth or ADC authentication** : Replace PROJECT\_ID with your Google Cloud project ID:

### Google Antigravity

#### Antigravity IDE and extensions

To configure the MCP server in Antigravity IDE or the Antigravity extension (such as in VS Code), select your authentication method:

### Google credentials

To install the MCP server using one-click setup:

1.  In the Agent panel, click the **Additional options** ( more\_horiz ) menu and select **MCP Servers** .
2.  Search for **Google Developer Knowledge** .
3.  Click the **Install** ( file\_download ) icon. Antigravity automatically configures the server and connects using your active Google credentials.

### API key

To configure an API key in Antigravity IDE or the Antigravity extension:

1.  In the Agent panel, click the **Additional options** ( more\_horiz ) menu \> **MCP Servers** \> **Manage MCP Servers** \> **View raw config** (or open `.agents/mcp_config.json` ).

2.  Add the following server configuration:
    
        {
          "mcpServers": {
            "google-developer-knowledge": {
              "serverUrl": "https://developerknowledge.googleapis.com/mcp",
              "headers": {
                "X-Goog-Api-Key": "YOUR_API_KEY"
              }
            }
          }
        }

#### Antigravity CLI

Configure the MCP server in your project's `.agents/mcp_config.json` file (or globally in `~/.gemini/config/mcp_config.json` ):

### Google credentials

    {
      "mcpServers": {
        "google-developer-knowledge": {
          "httpUrl": "https://developerknowledge.googleapis.com/mcp",
          "authProviderType": "google_credentials",
          "oauth": {
            "scopes": [
              "https://www.googleapis.com/auth/cloud-platform"
            ]
          },
          "timeout": 30000,
          "headers": {
            "X-goog-user-project": "PROJECT_ID"
          }
        }
      }
    }

### API key

    {
      "mcpServers": {
        "google-developer-knowledge": {
          "serverUrl": "https://developerknowledge.googleapis.com/mcp",
          "headers": {
            "X-Goog-Api-Key": "YOUR_API_KEY"
          }
        }
      }
    }

> **Tip:** If you're using the standalone Antigravity 2.0 application, go to **Settings** \> **Customizations** and click **Open MCP Config** under **Installed MCP Servers** to add your configuration.

### Claude Code

Run the following command in your terminal:

    claude mcp add google-developer-knowledge \
      --transport http https://developerknowledge.googleapis.com/mcp \
      --header "X-Goog-Api-Key: YOUR_API_KEY"

### Cursor

To configure Cursor, edit `.cursor/mcp.json` in your project root or `~/.cursor/mcp.json` for global access:

    {
      "mcpServers": {
        "google-developer-knowledge": {
          "url": "https://developerknowledge.googleapis.com/mcp",
          "headers": {
            "X-Goog-Api-Key": "YOUR_API_KEY"
          }
        }
      }
    }

### GitHub Copilot

> **Note:** If you're using the Antigravity extension in VS Code instead of GitHub Copilot, select the **Google Antigravity** tab.

#### Workspace settings

To configure GitHub Copilot in VS Code for a specific workspace, create or edit `.vscode/mcp.json` :

    {
      "servers": {
        "google-developer-knowledge": {
          "url": "https://developerknowledge.googleapis.com/mcp",
          "headers": {
            "X-Goog-Api-Key": "YOUR_API_KEY"
          }
        }
      }
    }

#### Global user settings

To make the server available across all VS Code workspaces, open your [User Settings (JSON)](https://code.visualstudio.com/docs/getstarted/personalize-vscode) and add the following under the `"mcp"` key:

    {
      "mcp": {
        "servers": {
          "google-developer-knowledge": {
            "url": "https://developerknowledge.googleapis.com/mcp",
            "headers": {
              "X-Goog-Api-Key": "YOUR_API_KEY"
            }
          }
        }
      }
    }

### Codex

To configure Codex CLI or the Codex agent, add the server configuration to `~/.codex/config.toml` (or your project's `.codex/config.toml` ):

    [mcp_servers.google-developer-knowledge]
      url = "https://developerknowledge.googleapis.com/mcp"
      http_headers = { "X-Goog-Api-Key" = "YOUR_API_KEY" }

> **Note:** After you change the configuration, the server may show a *not logged in* status. This is expected and won't affect your access.

### Other

To configure any other remote MCP client (such as JetBrains AI Assistant, Windsurf, Cline, Zed, Continue, or Claude Desktop), configure an HTTP transport server with the following settings:

  - **Server URL** : `https://developerknowledge.googleapis.com/mcp`
  - **HTTP Header** : `X-Goog-Api-Key: YOUR_API_KEY`

Standard JSON configuration template:

    {
      "mcpServers": {
        "google-developer-knowledge": {
          "url": "https://developerknowledge.googleapis.com/mcp",
          "headers": {
            "X-Goog-Api-Key": "YOUR_API_KEY"
          }
        }
      }
    }

## Verify the connection

Once configured, restart your AI assistant or reload its MCP servers. Then send a test prompt to verify that the tool integration works:

    How do I list Cloud Storage buckets using the Google Cloud Python SDK?

If the agent invokes `search_documents` or `answer_query` and returns information from Google documentation, your server is connected and active.

## Optimize context window and token usage

Retrieving full documentation pages into an AI model's context window consumes significant tokens. Ingesting multiple large documents can cause high token costs, increased latency, and context window overflow.

To ensure fast and cost-effective responses, follow these prompt engineering best practices:

  - **Rely on two-step retrieval** : Let the agent start by calling `search_documents` . This returns focused snippets (chunks) that often contain the exact syntax or API signature you need without consuming tokens for the entire page. Instruct your agent to call `get_documents` only when surrounding context is strictly necessary.

  - **Prefer `answer_query` for conceptual questions** : When you need a generated explanation or design comparison, direct your agent to use `answer_query` . This tool generates an answer directly from the Developer Knowledge corpus without returning full raw Markdown pages.

  - **Write specific, scoped prompts** : Avoid overly broad prompts such as "Explain all of Firebase". Instead, specify the target product, platform, and language:
    
        How do I write a Firestore transaction in Dart with error handling?

  - **Add custom agent rules** : Add project-level guidelines to your assistant's instruction files (for example, `.cursorrules` , `CLAUDE.md` , or `.github/copilot-instructions.md` ) to restrict automatic full-page fetches:
    
        When searching Google developer documentation, inspect search_documents
        snippets first. Do not call get_documents unless the snippet lacks
        necessary code context.

## Optional security and safety configurations

MCP introduces new security risks and considerations due to the wide variety of actions that you can do with the MCP tools. To minimize and manage these risks, Google Cloud offers default settings and customizable policies to control the use of MCP tools in your Google Cloud organization or project.

For more information about MCP security and governance, see [AI security and safety](https://docs.cloud.google.com/mcp/ai-security-safety) .

### Use Model Armor

[Model Armor](https://docs.cloud.google.com/model-armor/overview) is a Google Cloud service designed to enhance the security and safety of your AI applications. It works by proactively screening LLM prompts and responses, protecting against various risks and supporting responsible AI practices. Whether you are deploying AI in your cloud environment, or on external cloud providers, Model Armor can help you prevent malicious input, verify content safety, protect sensitive data, maintain compliance, and enforce your AI safety and security policies consistently across your diverse AI landscape.

When Model Armor is enabled with [logging enabled](https://docs.cloud.google.com/model-armor/configure-logging) , Model Armor logs the entire payload. This might expose sensitive information in your logs.

#### MCP request routing to Model Armor

Model Armor is available in [certain regions](https://docs.cloud.google.com/model-armor/locations) . When Model Armor is enabled and you use an MCP server in a jurisdiction that Model Armor doesn't support, the routing behavior of the call might be different for different MCP servers and might break data residency compliance for in-use and in-transit data. For more information about the behavior of individual MCP servers, see [Model Armor supported products](https://docs.cloud.google.com/mcp/model-armor-supported-products) .

#### Enable Model Armor

Follow the steps in [Integrate with Google and Google Cloud MCP servers](https://docs.cloud.google.com/model-armor/model-armor-mcp-google-cloud-integration) to enable Model Armor.

#### Configure protection for remote MCP servers

To help protect your MCP tool calls and responses you can use Model Armor floor settings. A floor setting defines the minimum security filters that apply across the project. This configuration applies a consistent set of filters to all MCP tool calls and responses within the project.

> **Tip:** Don't enable the prompt injection and jailbreak filter unless your MCP traffic carries natural language data.

Set up a Model Armor floor setting with MCP sanitization enabled. For more information, see [Configure Model Armor floor settings](https://docs.cloud.google.com/model-armor/configure-floor-settings) .

> **Note:** If the agent and the MCP server are in different projects, you can create floor settings in both projects (the client project and the resource project). In this case, Model Armor is invoked twice, once for each project.

See the following example command:

    gcloud model-armor floorsettings update \
    --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
    --enable-floor-setting-enforcement=TRUE \
    --add-integrated-services=GOOGLE_MCP_SERVER \
    --google-mcp-server-enforcement-type=INSPECT_AND_BLOCK \
    --enable-google-mcp-server-cloud-logging \
    --malicious-uri-filter-settings-enforcement=ENABLED \
    --add-rai-settings-filters='[{"confidenceLevel": "MEDIUM_AND_ABOVE", "filterType": "DANGEROUS"}]'

Replace `  PROJECT_ID  ` with your Google Cloud project ID.

Note the following settings:

  - `INSPECT_AND_BLOCK` : The enforcement type that inspects content for the Google MCP server and blocks prompts and responses that match the filters.
  - `ENABLED` : The setting that enables a filter or enforcement.
  - `MEDIUM_AND_ABOVE` : The confidence level for the Responsible AI - Dangerous filter settings. You can modify this setting, though lower values might result in more false positives. For more information, see [Model Armor confidence levels](https://docs.cloud.google.com/model-armor/overview#ma-confidence-levels) .

#### Disable scanning MCP traffic with Model Armor

To stop Model Armor from automatically scanning traffic to and from Google MCP servers based on the project's floor settings, run the following command:

    gcloud model-armor floorsettings update \
      --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
      --remove-integrated-services=GOOGLE_MCP_SERVER

Replace `  PROJECT_ID  ` with the Google Cloud project ID. Model Armor doesn't automatically apply the rules defined in this project's floor settings to any Google MCP server traffic.

Model Armor floor settings and general configuration can impact more than just MCP. Because Model Armor integrates with services like Vertex AI, any changes you make to floor settings can affect traffic scanning and safety behaviors across all integrated services, not just MCP.

#### Adjust Model Armor settings

If you're using [Model Armor](https://docs.cloud.google.com/model-armor/overview) to protect your application, you might encounter `403 PERMISSION_DENIED` errors for some queries. Because the Developer Knowledge MCP server only returns public documentation from trusted Google sources, we recommend setting Prompt Injection and Jailbreak (PIJB) filters to `HIGH_AND_ABOVE` confidence levels to reduce false positives. If your use case doesn't involve other tools that access private or sensitive data, you can also consider disabling PIJB filters.

## Troubleshooting

If you encounter issues connecting to or querying the Developer Knowledge MCP server, refer to the following troubleshooting matrix and resolution steps:

### Troubleshooting matrix

| Symptom or error                                                      | Likely cause                                                            | Resolution                                                                                                                                             |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `400 Bad Request: API key not valid`                                  | The API key string is missing, invalid, or malformed.                   | Verify that the API key was copied correctly and configured in the `headers` object with the `X-Goog-Api-Key` key.                                     |
| `403 PERMISSION_DENIED` : `Developer Knowledge API has not been used` | The Developer Knowledge API is not enabled in the Google Cloud project. | Enable the API in the Google Cloud console or run `gcloud services enable developerknowledge.googleapis.com` .                                         |
| `403 PERMISSION_DENIED: API target restriction`                       | The API key restriction list excludes the Developer Knowledge API.      | Update your API key restrictions on the Credentials page in the Google Cloud console to include Developer Knowledge API.                               |
| `401 UNAUTHENTICATED` or missing ADC credentials                      | Application Default Credentials are expired or not initialized.         | Run `gcloud auth application-default login --project=PROJECT_ID` to refresh local credentials.                                                         |
| `403 access_denied` / "Access blocked: authorization error"           | Your account is not listed as an authorized test user in OAuth consent. | In **Google Cloud console** \> **Auth Platform** \> **Audience** , add your email address under **Test users** .                                       |
| OAuth client error or invalid redirect URI                            | The OAuth client was created with an unsupported application type.      | Re-create your OAuth client ID with the type set to **Desktop app** .                                                                                  |
| `404 NOT_FOUND` on `/mcp` endpoint                                    | The API is not enabled for your project.                                | Enable the Developer Knowledge API in the Google Cloud console or run `gcloud services enable developerknowledge.googleapis.com` .                     |
| `429 RESOURCE_EXHAUSTED`                                              | You have reached your project's quota limit.                            | Check your [Developer Knowledge API quota](https://developers.google.com/knowledge/quota) usage in the console and request a quota increase if needed. |
| `403 PERMISSION_DENIED` with Model Armor                              | A false positive from the Model Armor PIJB filter blocked a safe query. | Set PIJB filter confidence to `HIGH_AND_ABOVE` in your Model Armor template settings.                                                                  |

### Resolve authentication and consent errors

  - **API key header configuration** : Verify that your MCP JSON configuration includes the `headers` section with `"X-Goog-Api-Key"` . Don't pass the API key as a query parameter in the URL.

  - **OAuth consent screen test users** : When creating a desktop OAuth client in a project with an external user type in testing mode, Google blocks access for accounts not listed under test users. Ensure your active Google email address is added under **Audience** \> **Test users** in the Google Cloud console.

  - **Quota and rate limits** : To monitor your daily and per-minute usage, go to **IAM & Admin** \> **Quotas & System Limits** in the Google Cloud console and filter by [**Developer Knowledge API**](https://console.cloud.google.com/apis/api/developerknowledge.googleapis.com/quotas) .

## Included documentation

See the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) for the full list of Google products and documentation repositories indexed by the server.

## Known limitations

  - **Public documentation only** : The server indexes only publicly available documentation listed in the [Corpus reference](https://developers.google.com/knowledge/reference/corpus-reference) . Internal documents, private repositories, and third-party resources are not included.
  - **English language** : The server indexes and returns documentation in English only.
  - **Network dependency and VPC Service Controls** : Because the Developer Knowledge MCP server is a remote hosted service, your client must have network connectivity to reach `https://developerknowledge.googleapis.com` .
      - **Inside Google Cloud VPC networks** : Public internet egress is not required. You can reach `developerknowledge.googleapis.com` privately without external IP addresses or Cloud NAT by routing traffic using [Private Google Access](https://cloud.google.com/vpc/docs/private-google-access) ( `private.googleapis.com` / `199.36.153.8/30` ) or a Private Service Connect (PSC) endpoint targeting the `all-apis` bundle.
      - **VPC Service Controls (VPC-SC)** : `developerknowledge.googleapis.com` is not supported on the Restricted VIP ( `restricted.googleapis.com` / `199.36.153.4/30` ) or PSC `vpc-sc` endpoints. If your VPC routes `*.googleapis.com` to `restricted.googleapis.com` , configure a specific Cloud DNS response policy or private DNS record for `developerknowledge.googleapis.com` to resolve to `private.googleapis.com` ( `199.36.153.8/30` ).
