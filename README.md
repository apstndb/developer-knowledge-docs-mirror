# Developer Knowledge Documentation Mirror

A local Markdown mirror of [Google Developer Knowledge](https://developers.google.com/knowledge/api) documentation, automatically updated via GitHub Actions.

This mirror covers the Developer Knowledge tree on `developers.google.com`:

- **API**: [`developers.google.com/knowledge/api`](https://developers.google.com/knowledge/api)
- **MCP**: [`developers.google.com/knowledge/mcp`](https://developers.google.com/knowledge/mcp)
- **Corpus reference**: [`developers.google.com/knowledge/reference/corpus-reference`](https://developers.google.com/knowledge/reference/corpus-reference)
- **Release notes**: [`developers.google.com/knowledge/release-notes`](https://developers.google.com/knowledge/release-notes)
- **RPC reference** under [`developers.google.com/knowledge/reference/rpc/`](https://developers.google.com/knowledge/reference/rpc/), discovered recursively from those seeds

`default_host` is `developers.google.com`. The crawl prefix is `developers.google.com/knowledge/`, which includes the pages above and excludes the separate [Knowledge Graph](https://developers.google.com/knowledge-graph/) corpus (`developers.google.com/knowledge-graph/`).

This repository does not mirror Gemini Enterprise Agent Platform pages such as [Connect to the Knowledge MCP server](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/connect-to-the-knowledge-mcp-server). That page belongs to a different product tree and is already covered by [gemini-enterprise-agent-platform-docs-mirror](https://github.com/apstndb/gemini-enterprise-agent-platform-docs-mirror).

## Authentication Setup

This tool requires Google Cloud credentials with access to the **Developer Knowledge API**. You can authenticate using either **Workload Identity Federation** (recommended) or an **API Key**.

### Option A: Workload Identity Federation (Secure, Recommended)

Workload Identity Federation (OIDC) is the most secure way to authenticate GitHub Actions to Google Cloud, as it eliminates the need for storing long-lived secrets or keys in GitHub.

#### 1. Configure Google Cloud

Run the following commands using the `gcloud` CLI (or configure them in the Google Cloud Console):

```bash
# 1. Create a Workload Identity Pool
gcloud iam workload-identity-pools create "github-pool" \
    --project="YOUR_PROJECT_ID" \
    --location="global" \
    --display-name="GitHub Actions Pool"

# 2. Create an OIDC Identity Provider for GitHub
gcloud iam workload-identity-pools providers create-oidc "github-provider" \
    --project="YOUR_PROJECT_ID" \
    --location="global" \
    --workload-identity-pool="github-pool" \
    --display-name="GitHub Actions Provider" \
    --attribute-mapping="google.subject=assertion.sub,attribute.repository=assertion.repository,attribute.actor=assertion.actor" \
    --issuer-uri="https://token.actions.githubusercontent.com"

# 3. Create a Service Account for the mirror tool
gcloud iam service-accounts create "gcp-docs-mirror-sa" \
    --project="YOUR_PROJECT_ID" \
    --display-name="GCP Docs Mirror Service Account"

# 4. Allow your GitHub repository to impersonate the Service Account
# Replace YOUR_PROJECT_NUMBER, YOUR_GITHUB_ORG, and YOUR_GITHUB_REPO with your actual values
gcloud iam service-accounts add-iam-policy-binding "gcp-docs-mirror-sa@YOUR_PROJECT_ID.iam.gserviceaccount.com" \
    --project="YOUR_PROJECT_ID" \
    --role="roles/iam.workloadIdentityUser" \
    --member="principalSet://iam.googleapis.com/projects/YOUR_PROJECT_NUMBER/locations/global/workloadIdentityPools/github-pool/attribute.repository/YOUR_GITHUB_ORG/YOUR_GITHUB_REPO"
```

> [!NOTE]
> Ensure that the Service Account has permissions to call the Developer Knowledge API (no special IAM roles are generally required other than basic API enablement in the project, but you may grant standard viewer roles if querying other GCP resources).

#### 2. Configure GitHub Secrets

Add the following repository secrets to your GitHub repository:

*   `GCP_WORKLOAD_IDENTITY_PROVIDER`: The full resource name of your provider:
    `projects/YOUR_PROJECT_NUMBER/locations/global/workloadIdentityPools/github-pool/providers/github-provider`
*   `GCP_SERVICE_ACCOUNT`: The email address of your service account:
    `gcp-docs-mirror-sa@YOUR_PROJECT_ID.iam.gserviceaccount.com`

---

### Option B: API Key (Simple Setup)

#### 1. Create the API Key

You can create a restricted API key using the `gcloud` CLI:

```bash
gcloud services api-keys create \
    --project=your-project-id \
    --display-name="Developer Knowledge API Key" \
    --api-target=service=developerknowledge.googleapis.com
```

#### 2. Configure GitHub Secrets

##### Via Web Interface
1.  Copy the generated API key.
2.  In your GitHub repository, go to **Settings** -> **Secrets and variables** -> **Actions**.
3.  Add a **New repository secret**:
    *   Name: `DEVELOPERKNOWLEDGE_API_KEY`
    *   Value: (Your API key)

##### Via GitHub CLI (`gh`)
If you have the `gh` CLI installed, you can set the secret directly:

```bash
gh secret set DEVELOPERKNOWLEDGE_API_KEY --body "YOUR_API_KEY"
```

---

## Setup Instructions

1.  **Configure GitHub Secrets**:
    *   Follow either **Option A (Workload Identity Federation)** or **Option B (API Key)** above to set up the necessary secrets in this repository.
    *   Working sibling mirrors such as [bigquery-docs-mirror](https://github.com/apstndb/bigquery-docs-mirror) use the same workflow auth pattern. This repository currently has neither WIF nor an API key configured, so scheduled runs fail before they fetch any pages.
2.  **Enable GitHub Actions**:
    *   Go to the `Actions` tab and enable workflows.
    *   The mirror updates daily at 18:00 UTC (03:00 JST), or you can trigger it manually via `workflow_dispatch`.

## Quota Management

The `gcp-docs-mirror-tools` is configured to respect quota limits, but simultaneous runs of multiple repositories will bypass these safety mechanisms. Always ensure that only one mirror update is running at any given time if they share the same API key.

## Manual Run

If you have Go installed locally, you can run the mirror script manually:

```bash
export DEVELOPERKNOWLEDGE_API_KEY=your_api_key
./mirror.sh
```

## Credits

This mirror system is powered by [gcp-docs-mirror-tools](https://github.com/apstndb/gcp-docs-mirror-tools).

## License

The documentation content collected in this repository is mirrored from Google Developers documentation according to the [Google Developers Site Policies](https://developers.google.com/terms/site-policies).
- Documentation content is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- Code samples are licensed under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0).
