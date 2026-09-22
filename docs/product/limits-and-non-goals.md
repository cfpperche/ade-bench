# Limits and non-goals

Owned honesty layer. Prefer adding lines here over silent over-claim in
capabilities.

## Not claimed in this repository (today)

- A stable interface: PiCode is **pre-alpha**; storage migrations and install
  paths may change between releases.
- Sandboxing of agents — they execute with the invoking user's permissions.
- First-class sub-agent routing in core.
- An auto-approve policy for managed Pi agents (explicitly undecided).
- Delivery that merges, runs project checks or publishes; integration and
  deployment execution queues are unavailable and publication stays `unknown`.
- Automations that run while the machine (and daemon) is off; missed slots
  catch up at most once.
- Off-site backup or sync.
- Native Windows server support: the supported install is Linux/WSL, with a
  Windows desktop shell wrapping WSL.
- Multi-tenant hosting for people you do not manage: sharing one box is the
  gateway topology, and a Linux user is a thin fence.
- Placeholder panes presented as features: tabs without a native editor read
  "in development — coming soon".

## License limits that matter for a public bench

PiCode is **PolyForm Noncommercial 1.0.0** (source-available, not OSI):
noncommercial use only; commercial use, selling access or bundling needs a
signed licence. In-tree installable pi packages declare MIT where their own
`LICENSE` says so. Do not describe PiCode as open source.

## Benchmark bias warning

Because PiCode is owned, operators can accidentally:

- write prompts that only PiCode understands
- intervene more or less than for competitors
- reuse long-lived tmux sessions or a warm database from a previous run
- measure `pi` (or another guest CLI) instead of the ADE, without recording
  which runtime and model ran
- treat the docs-fixture daemon (synthetic data, no real agents) as agent
  capability evidence

Mitigations: identical `prompt.md`, recorded interventions, a scratch data dir
per run, exact-session teardown, independent verifiers, and `run_config`
entries for guest runtime, model and execution surface.

## When to promote a claim

A capability may move to `status: claimed` in `capabilities.json` when:

1. it is true in the product tree you run for benchmarks (implementation or
   public docs — not a roadmap note),
2. you are willing to defend it under the same rules as competitor research
   (owned evidence is fine; fiction is not), and
3. it does not describe an undecided or placeholder behaviour as shipped.
