# grafana-tools

The Grafana observability CLI suite — `mcp-grafana`, `logcli`, `promtool`,
`mimirtool`, `tempo-cli`, `tk` (Tanka), and `grafanactl` — on the `PATH`.

`grafana-tools` installs the Grafana observability toolset as standalone binaries
under `/usr/local/bin`. Each binary is fetched from its upstream release during
the image build, so its presence on the `PATH` and its ability to report a
version are directly verifiable.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `grafana-tools` |
| Distro | all (upstream release binaries) |
| Binaries | `/usr/local/bin/`: `mcp-grafana`, `logcli`, `promtool`, `mimirtool`, `tempo-cli`, `tk`, `grafanactl` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-observability-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-grafana-tools:v2026.239.1628'
```

Then, inside the built image:

```bash
logcli --version         # Loki log query client
promtool --version       # Prometheus rule validation
mcp-grafana --help       # the MCP server
```

## Layout

- `charly.yml` — the `grafana-tools:` candy entity: the pinned
  `MCP_GRAFANA_VERSION` var, the per-binary install steps, and the `check:` steps.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Family skill: `/charly-coder:grafana-tools`
- `/charly-coder:devops-tools` — a common companion bundle in observability boxes
- `/charly-coder:kubernetes-layer` — pairs with Grafana for cluster observability
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
