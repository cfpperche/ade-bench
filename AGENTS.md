# Agent context — ADE Bench

This repository is **ADE Bench**: a reproducible harness and competitor-intelligence surface for comparing Agentic Development Environments (ADEs). **PiCode** is the owned reference product.

Agents working here must follow the boundaries below without re-asking.

## Repository map (this machine)

| Path | Role | Write? |
| --- | --- | --- |
| `/home/goat/ade-bench` (this repo) | Benchmark harness, competitor profiles, dashboard, marketing/intelligence | **Yes** (when the task requires it) |
| `/home/goat/picode` | **PiCode product** (browser-based ADE for Pi coding agents; Go + web/desktop shells) | **No — read only** |
| `git@github.com:cfpperche/picode.git` | Product remote | **No writes, no PRs, no pushes** |
| `git@github.com:cfpperche/ade-bench.git` | Bench remote | OK when the user asks to commit/push |

Also acceptable for **read-only** product research:

- Local clone: `~/picode`
- GitHub: `cfpperche/picode` (fetch/browse only)
- Public product docs: `https://cfpperche.github.io/picode/` (site links in `~/picode/README.md`)

## Hard rule: product repo is read-only

**You may read** `~/picode` (and its GitHub remote) to learn real product capabilities, architecture, docs, `CHANGELOG.md`, `Makefile`, ADRs, etc.

**You must not:**

- edit, create, or delete files under `~/picode`
- run `git commit`, `git push`, `gh pr create`, amend history, or change remotes in that repo
- install hooks, rewrite config, or “fix” things in place inside the product tree
- treat product `node_modules`/build output/`var/`/`.worktrees/` as a write playground

If product-facing claims need to land somewhere agents **can** write, use **this** repo:

1. Update `docs/product/` (especially `docs/product/capabilities.json`)
2. Run `python3 scripts/product/sync-picode-profile.py`
3. Run `python3 harness/bench.py check`
4. Optionally refresh `competitors/picode.json` notes/sources

Never invent PiCode features only inside the competitor JSON to look better on charts.

## What this bench repo is for

- Fair ADE comparison protocol (`SPEC.md`, `harness/`, `tasks/`)
- Competitor research profiles (`competitors/*.json`) — structured data, not scores
- Dashboard presentation (`apps/bench-dashboard`)
- Acquisition / battlecard intelligence (`marketing/`, `intelligence/`)
- Owned PiCode product surface **mirror** for the bench (`docs/product/`)

It is **not** the PiCode product source of truth. The product lives in `~/picode`.

## Canonical sources hierarchy (PiCode claims)

```text
~/picode  (product, READ ONLY)
    →  docs/product/  (bench-owned mirror you may edit)
    →  competitors/picode.json  (derived roster profile)
    →  dashboard radar / matrix
```

- `docs/product/capabilities.json` = machine-readable SSOT **inside the bench**
- Prefer aligning that SSOT with real product docs/code from `~/picode` (plus the public docs site) when enriching claims
- `runs/` = measured evidence only (gitignored); not a substitute for product docs

## Competitor profiles

- Source of truth for roster claims: `competitors/*.json`
- Rules: `docs/competitor-intelligence.md`, `competitors/README.md`
- Schema: `schemas/competitor.schema.json`
- Map: `reports/competitor-map-v0.1.md`
- Validate: `python3 harness/bench.py check`

**Class A** = local/multi-agent ADE peers (Orca, Herdr, Hive, Fusion, Maestri, …).  
**Class B** = enterprise platforms (e.g. Augment) — report separately.  
**Excluded example:** LandingAI-style document ADE (not software ADE).

Update workflow is **manual / on-demand** (no required cron job): re-check official sources, edit JSON, bump `last_reviewed` / `updated_at`, run `bench.py check`, update the map when comparison language changes.

## Dashboard charts (do not over-claim)

Capability Radar and Positioning Map scores are **heuristics from profile text/feature lists**, not harness results:

- Radar: roughly `min(100, feature_list_length × 12.5)` per feature group
- Positioning: keyword local-first score × orchestration list formula
- Real product quality lives in `runs/` + verifiers, not the radar polygon

PiCode can look “weaker” on the radar when `competitors/picode.json` is intentionally sparse. Fix by enriching `docs/product/` from **read-only** product research, then sync — not by fabricating bullets.

## Harness basics

```sh
python3 harness/bench.py check
python3 harness/bench.py list-products
python3 harness/bench.py list-inspectable
python3 harness/bench.py list-tasks
python3 harness/bench.py prepare --product <id> --task <task-id> --run-id <run-id>
# product works only in runs/<run-id>/worktree with prompt.md
python3 harness/bench.py verify runs/<run-id>
python3 harness/bench.py inspect --fixture mini-ade --run-id local-inspect
python3 harness/bench.py inspect --product <id> --run-id <id> --mode agent
python3 harness/bench.py inspect-verify runs/<id>
```

- Same prompt/fixture for comparable products
- Count human interventions
- Product marketing claims are not evidence

## Product surface scripts (bench repo)

```sh
python3 scripts/product/check-capabilities.py
python3 scripts/product/sync-picode-profile.py
python3 harness/bench.py check
```

## Useful paths

| Path | Content |
| --- | --- |
| `docs/product/` | Owned PiCode surface for the bench |
| `docs/inspect-harness.md` | OSS source-inspection protocol (Claude / Codex / Grok) |
| `inspect/` | Feature catalog, vendor-neutral prompt, hermetic fixtures |
| `docs/competitor-runbook.md` | **Playbook:** add/update/exclude competitors + publish Pages |
| `docs/competitor-intelligence.md` | Scope, source rules, research field meaning |
| `docs/competitive-intelligence.md` | Battlecards / signals |
| `docs/bench-roadmap.md` | Near-term ADE Bench roadmap (catalog, runtime model, harness, product deps) |
| `docs/acquisition-intelligence.md` | Marketing/acquisition |
| `docs/run-report-metrics.md` | Run metrics contract |
| `intelligence/current/signals.json` | Competitive signals |
| `marketing/registry/advertisers.json` | Acquisition advertiser aliases (1:1 with competitors) |
| `reports/archive/` | Retired artifacts (e.g. the Tachyon-era baseline), kept as history |

## Git / publish discipline (this repo)

- Prefer reversible local edits; confirm before force-push, history rewrite, or shared destructive ops
- `runs/*` is gitignored — keep smoke evidence local unless the user asks otherwise
- Commit/push only when the user asks

## Language

Respond in the user’s language when they write in Portuguese or English. Keep code/identifiers as in the repo.
