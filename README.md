# Developer Knowledge Documentation Mirror

A Markdown mirror of [Developer Knowledge](https://developers.google.com/knowledge/api), powered by [gcp-docs-mirror-tools](https://github.com/apstndb/gcp-docs-mirror-tools).

The mirror includes API and MCP guides, quickstarts, corpus reference, release notes, REST/RPC reference, and the available gcloud alpha developer-knowledge command reference. Host-scoped prefixes exclude Knowledge Graph and unrelated product trees. Narrow legacy Cloud prefixes allow redirect recovery when old links are discovered or seeded.

## Updates and authentication

The [workflow](.github/workflows/update-mirror.yml) runs daily at 17:20 UTC (02:20 JST the following day), or manually with workflow_dispatch. Documentation is stored in docs/, with metadata.yaml and logs/ describing the sync.

GitHub Actions uses Workload Identity Federation through the GCP_WORKLOAD_IDENTITY_PROVIDER and GCP_SERVICE_ACCOUNT repository secrets. The shared mirror identity admits apstndb-owned repositories ending in -docs-mirror on main. No API key is needed for this repository.

## Manual run

With Go installed, configure Application Default Credentials or set DEVELOPERKNOWLEDGE_API_KEY, then run:

```bash
./mirror.sh v0.3.1
```

The script prefers an existing local binary; remove or replace that binary if you need to change its version.

## License

Mirrored content follows the [Google Developers Site Policies](https://developers.google.com/terms/site-policies): documentation is [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) and code samples are [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).
