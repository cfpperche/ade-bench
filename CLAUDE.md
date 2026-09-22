# CLAUDE.md — ADE Bench

Follow **[AGENTS.md](./AGENTS.md)** as the primary agent context for this repository.

## Non-negotiable boundaries

1. **This repo** (`ade-bench`): you may edit when the task requires it.
2. **Product repo** (`~/picode`, remote `cfpperche/picode`): **read only**.
   - Do **not** write, commit, push, open PRs, or modify git state there.
   - Do **read** it freely to ground PiCode product claims (README, `docs/`, `docs-site/`, `internal/`, `web/`, `packages/`, `CHANGELOG.md`, `Makefile`, ADRs).
3. When product facts need to land in the bench, write to **`docs/product/`** (especially `capabilities.json`), then:

   ```sh
   python3 scripts/product/check-capabilities.py
   python3 scripts/product/sync-picode-profile.py
   python3 harness/bench.py check
   ```

## Quick orientation

- **Purpose:** fair ADE benchmark harness + competitor intelligence dashboard.
- **Protocol:** `SPEC.md`, `harness/bench.py`, `tasks/`.
- **Competitors:** `competitors/*.json` (validate with `python3 harness/bench.py check`).
- **PiCode SSOT inside the bench:** `docs/product/` (mirror of product knowledge; not a substitute for inventing features).
- **Charts:** radar/positioning are profile heuristics, not scored runs. See AGENTS.md.

## Claude-specific notes

- Prefer tools that read `~/picode` over guessing product capabilities.
- Do not “helpfully” apply fixes inside `~/picode` even if a bug is obvious; report findings or mirror allowed public/owned claims into the bench docs.
- If the user asks to change the product, clarify that product work belongs in `~/picode` under a separate session/policy — this session’s write scope is **ade-bench only** unless they explicitly change that rule in these files.
