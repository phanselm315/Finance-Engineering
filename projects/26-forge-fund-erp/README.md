# Forge — AI-Native Fund Accounting ERP

**Status:** 🔄 Active — core published and at rest; all funds reproduce byte-identical  
**Started:** June 3, 2026  
**Code:** Private build — details deliberately high-level here  

## What This Is

The most ambitious build of the journey so far: a from-scratch, AI-native fund
administration and investment-company accounting platform for private funds — the
category owned today by incumbents like Allvue, Dynamo, and eFront. Two bets define it.
First, audit-grade trust: every financial fact lives in an append-only, cryptographically
verifiable record, and every report can be replayed and proven byte-identical from that
record. Second, natural language as the eventual interface for querying and report design
— but only on top of a deterministic accounting core that makes the answers trustworthy.
The deterministic core is what's being built now.

This is where fifteen years of fund-accounting and audit domain knowledge meets everything
the previous 25 projects taught me about building with Claude. I've migrated funds onto
the incumbent platforms; this time I'm building the thing.

## How It's Being Built

The build process is the story I can tell publicly. A two-tier Claude workflow:

- **Cowork as architect and program manager.** Sessions where Claude and I resolve design
  questions in structured decision batches, grounded by my custom InvCoGAAP skill (ASC 946
  investment-company GAAP). Output: dated, versioned phase prompts and amendment files
  with an explicit precedence order.
- **Claude Code as the implementation engine.** Each phase prompt is handed off verbatim
  and implemented autonomously through explicit gates with hard stop conditions —
  "if any task would force X, STOP and report." No vibes-based progress.
- **Adversarial multi-agent review.** Independent reviewer agents — one engineering, one
  fund-admin SME — verify every load-bearing claim directly against the code, and an
  arbiter agent ranks the fix list. This review caught the demo overstating itself in
  several places; the fix principle became a rule: *fix what makes the demo a lie, defer
  what's merely incomplete.*
- **Persistent project memory.** A living lessons-learned file where every gotcha and
  every binding decision gets logged, so no session starts from zero.

Fifteen-plus build phases planned and executed across the run, with
the test suite (~140 passing tests, strict type-checking across the codebase) holding the
line throughout. The first working demo landed on schedule in early June; the build has since pushed past the demo into the accounting engines themselves.

## Current Milestone

The demo is real and running: sign in, then an LP-to-portfolio-company drill-in that
computes indirect ownership exposure deterministically from the event log, plus per-fund
browse. Since that first demo, the build has added the engines that make it an accounting
system rather than a graph:

- **Distribution-waterfall engine** — tiered GP/LP economics computed straight from the log.
- **Statement renderers and ASC 946 financial statements** — Statement of Assets &
  Liabilities, Statement of Operations, Schedule of Investments, and Financial Highlights,
  generated from the FactSet.
- **`verify-reproducibility`** — replays every fund's signed, hash-chained log and proves
  the projection-state hash byte-for-byte against the issued attestation, so tampering or
  drift is detectable after the fact.

**At rest and fully published (June 25).** The core is stable, not mid-build: `main`
equals `origin/main`, CI is green on both jobs, and all five fund anchors replay
byte-identical against their attestations. The last several sessions closed a run of small
backlog items cleanly rather than opening new territory:

- **LP self-service (closed Jun 24)** — an LP can see their own class economics plus a
  quarterly LP report. This is the investor-facing surface Wacker would hand a GP's LPs.
- **CI hygiene, web build gate, and a security patch (Jun 25)** — added a real web-app
  build step to CI (the root cause turned out to be a dev-mode flag leaking into the
  build, not the framework bug the backlog had assumed), bumped the toolchain, and applied
  the Next.js security patch that closes a known CVE chain.

The architecture underneath: an event-sourced ERP where each fund's git repo is the source
of truth, Postgres is a rebuildable projection cache, every event is Ed25519-signed and
hash-chained, and `forge verify-reproducibility` checks the attestations — running locally
via Docker Compose.

Next (scoped, not started): folding a fund's reapply step into the seed so a clean run
natively emits the canonical event log, byte-identical to its anchor. It's flagged as
anchor-sensitive, byte-exact seed surgery and deliberately deferred to its own dedicated
session with a checkpoint plan and a hard stop if byte-identity proves infeasible — a
one-way door, tr