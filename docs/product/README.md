# PiCode product surface (owned canonical source)

This directory is the **owned system of record** for PiCode capabilities as far
as this benchmark repository is allowed to assert them.

It is intentionally separate from:

- `competitors/picode.json` — **derived** research profile for the ADE roster
  and dashboard charts
- `runs/` — **measured** benchmark evidence
- marketing / battlecards — go-to-market narrative

## Rules

1. **Canonical first (inside the bench).** New product claims for the roster
   start here (Markdown + `capabilities.json`), then mirror into
   `competitors/picode.json`. Prefer grounding claims by **reading** the
   product repo at `~/picode` (and its public docs site / GitHub remote) —
   **never write** there. See root `AGENTS.md` / `CLAUDE.md`.
2. **No invention.** If a capability is not implemented or not ready to claim,
   mark it `status: not-claimed` or `placeholder`. Do not pad lists to look
   better on the Capability Radar.
3. **Public vs owned.** PiCode's repository is public, so claims may cite
   public product docs and source. Keep unshipped or undecided behaviour out of
   `claimed`.
4. **Radar axes map 1:1** to groups under `capabilities` in
   `capabilities.json` (same keys as `research.features` in competitor
   profiles).
5. **Dates.** When you change claims, bump `updated_at` in `capabilities.json`
   and, if you re-export to the profile, `research.last_reviewed` /
   `updated_at` on `competitors/picode.json`.

## Layout

| Path | Role |
| --- | --- |
| `overview.md` | What PiCode is (positioning, class, who it is for) |
| `capabilities.md` | Human-readable capability surface by ADE axis |
| `capabilities.json` | Machine-readable SSOT for feature lists / radar |
| `architecture.md` | High-level runtime model (owned, non-private) |
| `workflows.md` | Core operating loops the bench stresses |
| `limits-and-non-goals.md` | Honest limits, bias warnings, promotion rules |

## Workflow

1. Edit `capabilities.json` (and the Markdown views).
2. Export to the roster profile:

   ```sh
   python3 scripts/product/check-capabilities.py
   python3 scripts/product/sync-picode-profile.py
   python3 harness/bench.py check
   ```

3. Commit all three surfaces together.

If you only edit the Markdown, the radar polygon does not move: the sync script
reads `capabilities.json`, not this folder directly. Until you run the sync
script (or hand-update the profile), enriching docs alone will not move the
PiCode polygon.
