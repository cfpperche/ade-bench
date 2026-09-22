# PiCode architecture (owned sketch)

**Status:** owned, intentionally non-private
**Purpose:** orient maintainers and benchmark operators without publishing
implementation detail that the public docs do not already carry.

## Shape

```text
browser / desktop shell / phone PWA
        │  HTTPS + WebSocket + SSE
        ▼
one Go daemon (picode)
        ├── orchestration store: SQLite at ~/.picode/picode.db
        ├── tmux (one session per agent, one per project shell) ── PTY ── pi TUI
        ├── pi --mode rpc (JSONL stdio) ── structured chat for managed Pi agents
        ├── git / files / previews / delivery observation
        └── MCP servers, webhooks, automations, push
```

## Stack

| Layer | What |
| --- | --- |
| Runtime | Go (module `github.com/cfpperche/picode`), stdlib-first; WebSocket, PTY, MCP SDK, pure-Go SQLite, chromedp |
| Web | React + Vite + Tailwind workspaces for browser, desktop and mobile, xterm.js terminals |
| Interactive processes | tmux sessions owned by the daemon's own tmux socket |
| Storage | SQLite orchestration overlay; Pi session JSONL stays authoritative for conversations |
| Transport | HTTPS (mkcert or Tailscale cert), WebSocket for terminals/agent events, SSE for the change feed |
| Packaging | One binary with an embedded UI (or UI read from disk in dev); systemd user unit on Linux/WSL |
| Desktop | Tauri 2 + WebView2 shell on Windows, with the server still in WSL |

## Ownership boundary

PiCode is deliberately a thin layer over Pi and the vendor CLIs:

| Concern | Source of truth |
| --- | --- |
| Agent runtime | the user's installed `pi` |
| Conversations | Pi session JSONL |
| Credentials and Pi configuration | Pi's own auth/settings/package files |
| Interactive processes | tmux |
| Orchestration, inbox, delivery records | PiCode's SQLite database |

## Non-goals (stated by the product)

- Re-implementing the Pi TUI — it is embedded instead.
- Sandboxing agents — that is the runtime's trust model, not PiCode's.
- Hiding Pi — every GUI action maps to something inspectable in the terminal.
