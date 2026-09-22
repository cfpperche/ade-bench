# PiCode overview

**Status:** owned surface for ADE Bench (pre-alpha product)
**Last aligned with profile:** 2026-09-22

PiCode is a **browser-based Agent Development Environment (ADE) for Pi coding
agents**: one Go daemon serves a web UI that creates, configures and
orchestrates real `pi` processes across workspaces.

It is the **owned reference product** in this benchmark.

## What it is

- **Browser first.** The UI is the product surface; the terminal is one tab
  away, not the entry point.
- **Pi is not replaced.** Every managed agent is a user-installed `pi` process,
  launched either as the genuine TUI inside tmux or as `pi --mode rpc`
  structured chat.
- **Local-first.** The daemon runs as a systemd user service on Linux/WSL;
  orchestration state is a local SQLite file; provider credentials are the
  user's own.
- **Supervised, not unattended.** Blocking questions, approvals and finished
  runs land in one human inbox, reachable from desktop or phone.

## Class and runtime model

| Field | Value |
| --- | --- |
| Bench class | `A-local-ade` |
| Runtime model | `guest-cli` — the coding loop belongs to `pi` and the guest CLIs; PiCode owns the control plane |
| Guest runtimes | `pi` (managed: TUI or RPC), plus Claude Code, Codex, Grok, Hermes Agent, OpenCode, Muse Code, Antigravity, Omp as interactive terminals |
| Readiness | `owned-reference` |

## Who it is for

Solo developers running a few agents, terminal-averse users who still want
direct control, and teams hosting agents on a machine they manage (via the
optional shared-box gateway).

## Public surface

- Repository: <https://github.com/cfpperche/picode>
- Documentation: <https://cfpperche.github.io/picode/>
- License: **PolyForm Noncommercial 1.0.0** (source-available, not OSI);
  in-tree installable pi packages carry MIT where their own `LICENSE` says so.

## Status caveats

PiCode is **pre-alpha**: interfaces, storage migrations and installation paths
may still change between releases. Pin a release tag for any reproducible
comparison. See `limits-and-non-goals.md`.

## What “done” means for PiCode work

A change is not done when an agent stops talking. It is done when:

- the change is visible in the browser surfaces the product already ships
  (chat or terminal, inbox, files/diff, delivery), and
- the repository's own gates pass (`fmt-check`, `vet`, tests, docs parity), and
- the changelog fragment and handoff note exist for user-visible changes, and
- claims in this folder are updated when the capability surface changes.

The bench adds one more gate: an identical task prompt, an independent
verifier, and a recorded intervention count.
