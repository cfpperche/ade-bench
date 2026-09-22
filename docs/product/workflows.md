# PiCode core workflows

Owned operating loops that the ADE Bench is designed to stress. Keep these
aligned with `harness/` protocol language.

## 1. Create and run an agent

1. Open the daemon in a browser (`https://localhost:8445` by default).
2. Add a workspace (a registered folder) or create a free agent.
3. Create an agent inside it: name, CLI (default `pi`), model, provider,
   working directory.
4. Press **Run**. Closing the tab does not stop the agent — tmux owns the
   process.

## 2. Watch and steer

- Structured chat for managed Pi agents, or the real Pi TUI tab for the same
  session.
- `steer` and `follow_up` reach an agent while a turn is still running; a queued
  prompt waits for the agent to settle.
- Session commands (`/tree`, `/fork`, `/resume`, `/compact`, `/export`, …) are
  surfaced in the UI and map onto Pi's own session behaviour.

## 3. Answer from one inbox

- Blocking questions and approvals, settled runs with nobody watching, and
  unexpected exits all become inbox items.
- A reply reaches a managed agent as a follow-up, a TUI agent inside its
  terminal, or a terminal agent through its receiver — and only counts once the
  session record shows the user row.

## 4. Review a change

1. Files / Changes shows the working tree with per-file counts, narrowed to the
   agent that edited it.
2. Open the file, read the diff, save edits.
3. Git actions are **composed**: Prepare types the command, Run is offered only
   when no agent is mid-turn, and destructive tiers ask for a typed phrase.
4. A pull-request view reads `gh` output; PiCode never stores a GitHub token and
   never opens a PR by itself.

## 5. Declare delivery

- An agent registers a revision-bound change and requests review from its own
  terminal (`picode delivery …`) or through the delivery MCP family.
- PiCode observes local refs and receipts and labels the change; integration
  and deployment execution queues are explicitly unavailable.

## 6. Automate

- Create a rule with a cron schedule or a webhook secret, or draft one from a
  chat command.
- Runs appear as normal sessions with an inbox result; skipped runs explain
  themselves (busy, rate cap, agent in terminal) and failures name the cause.

## 7. Supervise from a phone

- Install the PWA, pair the device, and use the Now tab (needs-you first),
  inbox triage, and terminal attach with the accessory key bar.
- Push notifications fire only when nobody is watching on the host.

## 8. Benchmark loop (this repository)

1. `python3 harness/bench.py prepare --product picode --task <id> --run-id <id>`
2. Point the product **only** at `runs/<id>/worktree` with `prompt.md`.
3. `python3 harness/bench.py verify runs/<id>`
4. Fill `run_config` / intervention fields before any public comparison —
   including the guest runtime (`pi` vs a guest CLI) and the model, because the
   coding loop belongs to the runtime, not to the ADE.

Practical note for operators: use a scratch instance with its own data dir and
its own tmux socket for runs, and stop those exact sessions afterwards —
PiCode's terminals are designed to survive the browser, so they will survive a
careless benchmark teardown too.
