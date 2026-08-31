# Forge — AI-Native Fund Accounting Platform

**Status:** ⏸️ At rest since August 3, 2026 — the Command Center front end and every attested surface through nested/parallel vehicles landed on main  
**Started:** June 3, 2026  
**Last updated:** August 31, 2026  
**Code:** Private build — details deliberately high-level here  

## What This Is

Forge is an AI-native fund accounting platform for funds and their portfolio companies,
built on one idea: books that replay byte-identical from a signed event log are books that
are cheap to audit and easy to defend.

Most emerging managers can't easily prove how they got a number — a mark, a capital
balance, a fee calc — until an auditor or LP asks, and then it's a scramble. Forge fixes
that at the source: every economic event, from a capital call down to a portfolio
company's operating expense, is recorded once on a signed, reproducible ledger, and the
books follow by rule. The result is audit-ready books as a deliverable, and a valuation
you can defend without a fire drill.

I've migrated funds onto the incumbent platforms — Allvue and Dynamo — and worked inside
proprietary fund-admin systems besides. This is the platform I'd have wanted on those migrations.

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

The architecture underneath: an event-sourced core where each fund's git repo is the
source of truth, Postgres is a rebuildable projection cache, every event is Ed25519-signed
and hash-chained, and `forge verify-reproducibility` replays every fund's log and proves
the projection-state hash byte-for-byte against the issued attestation — so tampering or
drift is detectable after the fact. ASC 946 financial statements (Statement of Assets &
Liabilities, Statement of Operations, Schedule of Investments, Financial Highlights),
distribution waterfalls, and per-class LP economics are all derived from that one log.

The front end is a Next.js 15 / React 19 / TypeScript-strict / Tailwind app, server-first
on the App Router and wired straight to the FastAPI core — no separate reporting database
to reconcile against. It already serves live, backend-wired ASC 946 statements, the
distribution waterfall, partners' capital and per-LP highlights, the ingest tie-out and
queue, and value-creation demos, each cell carrying a provenance color so a reader can see
at a glance what's attested versus derived versus still pending. The unified "command
center" landing view I designed in Claude Design (Fable) is now ported and live on main,
behind the same type-check and lint gates as the rest of the build, and the tables it
fronts carry their own filter, sort, and column-drag. Working prototype throughout; the
read-only viewer never gets a write path into the ledger.

## Where It Stands

| Date | Shipped | Verification state |
|------|---------|-------------------|
| Early Jun | First working demo: sign-in, LP→portco drill-in computing indirect ownership from the event log, per-fund browse | On schedule |
| Mid Jun | Distribution-waterfall engine; ASC 946 statement renderers off the event-derived fact store | Tests green |
| Jun 24 | LP self-service: per-class economics + quarterly LP report | CI green |
| Jun 25 | CI web-build gate; Next.js security patch (known CVE chain) | At rest: five funds byte-identical, both CI jobs green |
| Jun 26 | Byte-exact seed surgery — reapply step folded into the seed | Zero event bytes changed; CI green |
| Late Jun | Per-class LP economics attested; live multi-class fund; MFN better-of-terms logic | Each anchor move: explicit go, pre-planned reseed, triple verification |
| Jun 30–Jul 1 | Carried interest provable off the attested log; LP display serves attested rows | Six consecutive fresh-process reproducibility runs; all five funds byte-identical; 620 tests passing (0 failed); lint clean |
| Jul 3 | Value-creation layer increments: predicted, thesis-mapped levers paired by hash to the realized EBITDA-to-equity bridge | CI green; anchor-neutral — pin gate confirmed no attested code touched; suite grew past the 620 baseline |
| Jul 6 | Portfolio-company chart-of-accounts v2 reseed | Anchor move: pre-planned reseed, verified |
| Jul 7 | Statement of Cash Flows (ASC 946 / ASC 230), direct view plus the mandatory reconciliation | LIGHT / read-only / anchor-neutral: reads ORM models only, zero bytes under `accounting/`, pin gate proves all five anchors frozen; tri-reviewed |
| Jul 7 | Command-center landing view designed in Claude Design (Fable); D0 port spec locked over the already-live Next.js 15 / React 19 / Tailwind app | `web/`-only, no `forge/` touched; port gated at D0 — spec done, component code not yet written |
| Jul 13 | Net-working-capital rollforward promoted to an attested surface (`AttestedNwcRollforward`) | RESEED-CLASS anchor move: pre-planned reseed; merged via PR #5, CI green |
| Jul 14 | LP-surface audit: whole-fund Financial Highlights tiers, an IRR ruling, LP-inputs tier badges | Surface work over the attested log; CI green |
| Jul 15 | Valuation-source scope (F5) tri-reviewed — reclassified HEAVY → predicted-LIGHT, rulings of record, FINAL ready | Scope locked; the build is the next step |
| Jul 16 | Valuation-source (F5) built and merged to main (PR #6); Command Center front end ported and landed on main (PR #7) | F5 independently verified and closed out; reconciliation trustworthy; CI green |
| Jul 17 | A3 side pockets — LP × instrument participation with an attested cash-flow ledger | New attested surface; scope FINAL after tri-review + 5 rulings before any code |
| Jul 18–23 | Nested/parallel vehicles — co-invest widened into a general primitive; two worked examples (co-invest sleeve, feeder) | Scope FINAL; both examples shipped; CI green |
| Jul 23–24 | Front-end table interactions — filter/sort/column-drag across Portfolio, Key Figures, LP roster, Ingest Queue, Tie-Out, fund detail | Shipped in two waves; scope FINAL after a 4-pass review |
| Jul 24 | Journal view — page-scoped client-side sort, with CSV export following the sort | Extracted as a client component with the server-side filter and pagination byte-identical, independently diffed twice; 129/129 web tests, typecheck and lint clean |

One environmental caveat on the Jun 30 verification: the local Docker engine crashed
repeatedly on the monolithic test run, so the suite ran per-file per the standing Windows
protocol; the reproducibility core covers the stability concern independently.

### At rest since August 3

Nothing has been committed since August 3. That is a stopping point, not a stall: the
Command Center front end, the valuation-source scope, side pockets, and nested/parallel
vehicles all landed and closed out, and what remains in the queue — the ingest map-book
work, and a content-safety review of two dozen old unmerged branches — is waiting on
attention rather than on anything unresolved.

One late-July recount belongs in the record. The ingest map-book gate had been carried
for weeks as "one portfolio company has rule history." Grepping every fund and vehicle
log directly turned up zero. The corrected number moves that gate further out of reach,
not closer, which is exactly why the flattering reading was the easy one to keep.

### A failure worth recording

The July 3 increment was pushed before its independent pre-publish pass was run, and CI
went red for about thirteen minutes on a type-check error the branch's close gate hadn't
caught — it ran the linter but not the type checker. It was fixed forward, verified
locally the second time, and is green now. The lesson is recorded where it belongs: the
close gate must run the type checker too, and a "clean" self-report is a claim to verify,
not to trust.

## Key Decisions

**Domain expert in the loop, on the record.** Claude drafts the accounting logic; I
correct it as the CPA — and the corrections get logged, not just applied. The marketplace
scan found no existing Claude skill or tool that does fund accounting at all. That gap is
the opportunity.

**Gates, not momentum.** Big phases get subdivided rather than rushed at the end of a long
context window, and irreversible steps get their own focused, pre-planned sessions.

**Match the ceremony to the blast radius.** Not every change deserves the full heavy-review
apparatus. Work that can move an attested anchor gets adversarial review and my explicit
go; purely additive, off-surface work gets a lighter tier and ships faster. The mechanical
test — does the attested surface change, does any anchor move — tells an unattended loop
exactly where it must stop and ask for a human.

**Claims must match code.** After the adversarial review, demo claims that the code
couldn't back were treated as bugs of the highest severity.

**The strategic frame.** Forge is the reproducible bottom layer of a larger system. The
buyer is a GP, reached through Wacker Advisors acting as an outsourced operational CFO;
the thesis is that *reproducible-for-anyone* makes audit support materially cheaper, with
pricing tied to provable correctness rather than hours. The end state is continuous
reconciliation — the books are never "closed" because they're always provable.

## Lessons Learned

An AI can write a working, tested accounting core in days — if a domain expert designs
the decision process around it. Every hard problem so far has been an accounting judgment
or a process-design question, not a coding question. The two-tier prompt-file workflow
(architect sessions producing versioned prompts, implementation gated behind verification)
is the most repeatable engineering pattern I've found in six months of building.

And: adversarial review is non-negotiable. The system was confidently wrong in ways that
only an agent tasked with *proving the demo dishonest* actually caught.

---

*Part of [Finance Engineering](../../README.md)*
