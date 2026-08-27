# Developer Knowledge Documentation Mirror

This repository mirrors official Developer Knowledge documentation as Markdown using [gcp-docs-mirror-tools](https://github.com/apstndb/gcp-docs-mirror-tools).

The mirror covers:

- Developer Knowledge API and quickstart documentation under `developers.google.com/knowledge/`
- Developer Knowledge MCP documentation in the same documentation family
- The available `gcloud alpha developer-knowledge` command reference
- Legacy `cloud.google.com` links for that command family, which are followed to their canonical `docs.cloud.google.com` destinations

The stable and beta `gcloud developer-knowledge` command families are not included because those pages are not currently available through either the Developer Knowledge API or the public documentation site.

## Automatic updates

The [update workflow](.github/workflows/update-mirror.yml) rebuilds the mirror daily at 17:20 UTC (02:20 JST on the following day) and can also be run manually. Generated documentation is committed under `docs/`, with run metadata and diagnostics in `metadata.yaml` and `logs/`.

The workflow requires the `DEVELOPERKNOWLEDGE_API_KEY` repository secret. It also supports Workload Identity Federation when `GCP_WORKLOAD_IDENTITY_PROVIDER` and `GCP_SERVICE_ACCOUNT` are configured.

## Manual run

Set a Developer Knowledge API key, then run the pinned mirror tool version:

```bash
export DEVELOPERKNOWLEDGE_API_KEY=your_api_key
./mirror.sh v0.3.1
```

## License

The mirrored documentation is subject to the [Google Developers Site Policies](https://developers.google.com/terms/site-policies):

- Documentation content is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- Code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).
