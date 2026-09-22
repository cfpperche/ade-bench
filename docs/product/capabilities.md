# PiCode capabilities

Human-readable view of the owned capability surface. The machine-readable SSOT
is [capabilities.json](./capabilities.json). Keep them in sync.

Status vocabulary: `claimed` (true in the product today) · `placeholder`
(partial/undecided) · `not-claimed` (explicitly not a capability).

## Agent support

What runtimes PiCode can drive.

**Claimed:**

- Real `pi` processes as the managed runtime — TUI in tmux, or `pi --mode rpc`
  structured chat.
- An agent CLI catalog beyond Pi (Claude Code, Codex, Grok, Hermes Agent,
  OpenCode, Muse Code, Antigravity, Omp) as interactive terminals with activity
  reporting where the vendor exposes a signal.
- Per-agent provider, model and thinking level passed to `pi`; Pi keeps
  ownership of its own auth file.

**Not claimed:**

- First-class sub-agent delegation in core. Roles and delegation ship as opt-in
  pi packages, not daemon routing.

## Orchestration

How work is split, queued and supervised.

**Claimed:**

- Agent fleets across workspaces (plus free agents).
- Durable task delivery: a prompt waits for settle; `steer` and `follow_up`
  reach a running turn.
- One human inbox for questions, approvals, results and unexpected exits.
- Inter-agent messaging broker over MCP plus a durable peer mailbox.
- Automations on cron or webhook with jitter, watchdog, cost cap and one
  catch-up run.
- A canvas board of agent/terminal/note/file/diff panels, where edges grant a
  contact rather than a transcript.

**Not claimed:**

- An approval policy of its own: PiCode surfaces the dialogs and permission
  prompts the runtime reports; auto-approve is undecided.

## Workspace isolation

How agent work is separated on one machine.

**Claimed:**

- Per-agent working directory (workspace folder plus optional `workPath`).
- One tmux session per agent and per project shell, surviving browser and
  daemon restarts.
- A private per-agent Pi session directory.
- Git worktree visibility plus composed create/prune/remove actions under
  `<root>/.worktrees/<name>`.

**Not claimed:**

- Agent sandboxing. Explicit non-goal: agents run with the invoking user's
  permissions. Containers appear only in the shared-box gateway topology.

## Review and shipping

How a change is inspected and handed off.

**Claimed:**

- Working-tree review with per-agent attribution (which files this agent
  touched).
- File browse and edit with Save, plus sandboxed HTML/markdown previews.
- Commit graph with refs, remotes and worktrees, and per-file patches.
- Composed git actions with risk tiers; tier C requires a typed phrase.
- Delivery declarations with integration observation.
- Cross-CLI session handoff with lineage.

**Boundary to respect in reports:** PiCode never merges, never runs project
checks and never publishes; publication state stays `unknown`.

## Remote and mobile

How the same fleet is supervised away from the desk.

**Claimed:**

- A four-tab mobile PWA (Now, Inbox, Work, More).
- In-tree push notifications for blocked agents, blocking inbox items and
  finished runs, suppressed while a host browser is present.
- Per-device pairing with one-use codes and revocable devices.
- Remote access on a private network (mkcert or Tailscale) with persisted bind
  and public-URL settings.
- A shared-box gateway mapping tailnet identities to Linux users.
- A Windows desktop shell (server still runs in WSL).

## Context and memory

What is remembered, and who owns it.

**Claimed:**

- SQLite orchestration overlay; conversations remain Pi's session files.
- SSE change feed with a typed event row per mutation and cursor reset past
  retention.
- Cross-CLI session read and write paths.
- Per-CLI long-term memory panes with declared tiers (`editable`, `readonly`,
  `none`, `unknown`).
- An encrypted provider-credential vault for PiCode and the guest CLIs.
- Backup/restore of PiCode data with atomic swaps.

## Integrations

How PiCode attaches to the rest of the toolchain.

**Claimed:**

- MCP servers exposing PiCode tools (computer, browser, inbox, checklist,
  delivery).
- A connector pane that writes each vendor's own MCP configuration.
- HMAC-signed webhooks with ordered retries.
- A package pane for Pi and the guest CLIs, plus MIT installable packages
  in-tree.
- A browser extension that hands page context to an existing agent.
- An optional local model (llama.cpp) manager.

## How to change this file

Edit `capabilities.json` first; this Markdown mirrors it. Then run
`python3 scripts/product/check-capabilities.py` and
`python3 scripts/product/sync-picode-profile.py`.
