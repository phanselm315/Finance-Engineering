# Sass Factory — Gated Software Factory

**Status:** 🔄 Active — self-advancing loop sustained across repeated backlog cycles; gate chain hardened further  
**Started:** June 25, 2026  
**Code:** Private build — kept high-level here; clean-room by design  

## What This Is

A gated software factory: spawn sandboxed coding agents at a git repo, watch them work
live, and gate everything at the merge boundary so nothing ships unchecked. In one line —
a loop of loops that builds, reviews, tests, and ships software end to end.

It fuses two influences. From **Warren** (Jaymin West's open-source control plane): the
shape — a run record, a per-run event stream you can tail live, an isolated workspace, an
agent spawn, and a reap that opens a PR. From **Forge** (my fund-accounting ERP build): the
discipline — architect sessions → gated phases → adversarial multi-agent review, with the
review synthesis governing over the plan. Built clean-room from my own understanding of the
pattern, not ported from anyone's code; borrowed ideas are credited in the repo.

The defining choice: keep Warren's live observability but **invert its merge philosophy**.
Warren trusts the infrastructure and automerges; Sass Factory trusts the *gate*. The reap
is a pluggable gate chain, and a run merges only on all-green — and even then it proposes a
PR rather than self-merging, so the one-way door stays reversible.

## Architecture

- **Control plane** — a FastAPI service over a raw-`sqlite3` run store: create a run, read
  it back, and stream its events live (NDJSON `?follow=1`) until the run is terminal. No
  ORM; the SQL is right there on purpose.
- **Event log** — append-only, per-run `seq`-ordered. A single run streams
  `run.created → running → agent.stdout → agent.tool_use → gate.result → review.verdict →
  merged`. That one cursor is what makes live tailing, the review-verdict feed, and later
  replay all fall out cheaply.
- **The gate chain (the reap).** Gate 1 is deterministic `check-all`: a ruff format/lint
  baseline, mypy strict types, a coverage ratchet (the floor only goes up — currently 93%),
  and a duplicate-code gate. Gate 2 is an **adversarial review agent** that reads the diff
  and votes merge or block. All-green proposes a PR; any block stops the run with a report.
- **The self-advancing loop (`factory/`).** A driver reads an ordered backlog, runs each
  deliverable through a headless coding agent, gates on `check-all`, commits on green, and
  advances to the next — no human shuttling prompts between sessions. The queue *is* the
  handoff.

## Current Milestone

**Full self-advancing cycle, end to end (Jul 3).** The loop has now run a complete cycle on
its own: the driver pulled an ordered backlog, ran each deliverable through a headless coding
agent, gated on `check-all`, committed on green, and advanced — no human shuttling prompts
between sessions. The gate chain also gained a new check, tightening the merge boundary further.
Proof-before-merge held throughout: the factory kept building only what its own gates would pass.
(Specifics tracked in the private build repo.)

**Update (Jul 13).** The loop has kept running unattended since — shipping a run of
gate-hardening backlog items through roughly #37 (fail-closed on a no-op commit, scrubbing
config vars so they can't flip a review verdict, retry-then-fail-closed on a flaky check,
closing the agent's push-bypass), with #38–44 already queued. The end-to-end cycle isn't a
one-off; it's the factory's steady state. Two independent review passes have prompted me to
weigh a different direction — pointing the gate chain at numeric-invariant
fund-reconciliation work — which I'm still evaluating.

## Key Decisions

**Trust the gate, not the agent.** The whole point is that an agent's output is assumed
wrong until the environment proves it right. Deterministic checks plus an adversarial
reviewer are that proof; the agent's confidence counts for nothing.

**Propose a PR, don't self-merge.** Shipping to `origin` is a one-way door, so the reap
stops at a proposed PR — reversible by default, even inside an unattended loop.

**Dogfood it.** The first thing the factory builds is itself: its own backlog runs through
its own control plane and gate chain. If it can't reliably ship its own features, it isn't
ready to ship anything else.

**Clean-room, provenance clean.** Built from my understanding of the pattern rather than
ported from the MIT-licensed original, with influences credited — to keep commercialization
options open.

## Lessons Learned

This is the gated build-loop pattern from Forge, generalized. Forge was a nested-loop
system built to
produce one product, with me still running the build. Sass Factory extracts that build
process into a reusable, self-advancing system.

The hard problems were boundaries, not code: where the one-way doors are, what a gate must
guarantee before it lets a change through, and how an unattended loop fails *closed* instead
of shipping something unchecked. Same lesson as Forge, one level up.

---

*Part of [Finance Engineering](../../README.md)*
