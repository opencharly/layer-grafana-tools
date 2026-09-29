# AGENTS.md — layer-grafana-tools

Standalone candy repo for the `grafana-tools` layer — the Grafana observability
CLI suite (`mcp-grafana`, `logcli`, `promtool`, `mimirtool`, `tempo-cli`, `tk`,
`grafanactl`) installed as standalone binaries under `/usr/local/bin`. The candy
lives in `charly.yml` at the repo root and projects the `grafana-tools` skill
entity (`family: coder`).

Canonical files:

- `charly.yml` — the `grafana-tools:` candy entity and the `grafana-tools-skill:`
  skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-coder:grafana-tools` — the owning skill: the tool catalog, what each
  binary does, and the install story. Load before editing or troubleshooting the
  layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: one file check
  per binary under `/usr/local/bin`, plus the `logcli --version` and
  `promtool --version` exit checks.
- Every install step fetches from an upstream release; a version bump or a
  binary rename is a change in both the install step and its `check:`.

## Modify this repo

- Edit the `grafana-tools:` candy entity in `charly.yml`; keep the matching
  `grafana-tools-skill:` entity in step with it.
- When adding or removing a tool, add or remove its install step, its file
  `check:`, and its row in the skill's catalog together.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
