# Finance Engineering

I solve finance operating problems for private capital.

For fifteen years I've worked inside the institutions that run private capital's finance function — Big Four, Northern Trust fund administration, a long-standing internal PE investment program at Kirkland & Ellis — on fund and portco accounting, controllership, compliance, and reporting: ASC 946 statements, ERP implementations, close processes, audit and custody readiness, distribution waterfalls, and LP reporting.

Today AI lets me encode those operating models into software. That's the only reason AI is in this repo at all — it's the newest implementation layer for work I've been doing my whole career.

This is the public body of work behind that.

---

## Selected Work

Three builds carry the thesis. Each runs on synthetic or anonymized data with production-style logic — this is a lab, not a client environment.

### [Forge — AI-Native Fund Accounting Platform](./projects/26-forge-fund-erp/)

**Problem.** Fund administration is built on reconciliation: the same capital activity keyed into four systems, then proven to agree every close. The duplicate sources of truth *are* the cost.

**Approach.** One replayable, deterministic accounting core. ASC 946 statements, distribution waterfalls, and per-class LP reporting are *derived* from it, not reconciled into agreement.

**Result.** Five demo funds replay byte-identical from a signed event log — statements, waterfalls, and per-class LP economics all derived from one attested source, with 600+ tests behind it. I've migrated funds onto Allvue, Dynamo, and eFront; this is the platform I'd have wanted on those migrations.

### [Portfolio-Company Value-Creation Suite](./projects/20-value-creation-suite/)

**Problem.** Operational-finance diagnostics for portfolio companies die as slides at the end of an engagement. The work isn't reusable and never rolls up to the fund.

**Approach.** Four diagnostics, each pairing a deterministic engine with a narrow LLM judgment layer, each rolling a single-portco win up to a fund-level EBITDA bridge: Working Capital (AR / trapped-cash, collections outreach gated behind human approval), Freight (shipment history re-priced against live carrier rates), Inventory (ABC × XYZ segmentation, safety/cycle stock, fund-wide pooling), and Procurement (spend classification, tail/maverick risk, fund-wide negotiation playbook).

**Result.** The diagnostic becomes a reusable fund asset instead of a one-time deliverable. Code is public for all four.

### [Wacker Advisors OS](./projects/16-wacker-advisors-os/)

**Problem.** A one-person CFO/CCO practice still has to run compliance calendars, deliverable tracking, and recurring document work without a back office.

**Approach.** The firm's operating model made executable — compliance calendars, deliverable tracking, document automation, with the recurring judgment encoded as rules and dedicated domain skills for SEC private-funds compliance and ASC 946 accounting. All compliance output is reviewed and owned by me; the system accelerates, it doesn't decide.

**Result.** It runs the firm's own back office today — intake through engagement letter through invoicing — built ahead of the first client engagement.

---

## In Production Use

Two earlier builds have real users, today:

- **[Monthly Financials Builder](./projects/09-monthly-financials-builder/)** — turned a 45-minute monthly board-package assembly into a 10-second command. In monthly use by a nonprofit board.
- **[Parish Bookkeeping System](./projects/11-parish-bookkeeping-system/)** — documented 30 years of undocumented close process across multiple entities, automated the QuickBooks workflows, and handed the system off.

---

## What is Finance Engineering?

Finance transformation knows *why* a finance organization should work a certain way — where truth lives, what evidence an accounting event needs, how a close survives an audit — but it stops at slideware. Software engineering can build the system but doesn't carry the operating model. A finance engineer does both: design the operating model **and** encode it into software — the rules, controls, and "we don't book it until X" that normally live in a senior controller's head, made executable, replayable, and auditable. The model (Claude, Grok, ChatGPT) is rented and commoditizing; the durable asset is the encoded judgment, the checks, and the audit trails around it — the layer institutional finance has always cared about most.

## How I Build

Start with the operating model, not the technology: why does this process exist, where does the truth live, what evidence and approvals does the event need? Software comes last, and only for the parts that earn it. One instinct runs through everything here: output has to be verifiable and hard to silently degrade — gates inside gates, human approval before any agent touches the outside world, replayable cores where a discrepancy is always a real signal. That's a controls habit, not an AI one.

Every build — including earlier and personal projects — is in [`projects/`](./projects/); the chronological record is in [`LOG.md`](./LOG.md).

---

## Additional Research

Adjacent work — good builds, but supporting evidence rather than the main thesis.

- **[Sass Factory — a Gated Software Factory](./projects/28-sass-factory/)** — a build loop where nothing merges until it's proven: coding agents in isolated git clones, every change gated at the merge boundary by deterministic checks plus an adversarial review agent. The separation-of-duties instinct of a finance close, turned into a machine that builds.
- **[007 — Multi-Agent Equities Research](./projects/17-007-trading-agent/)** — a from-scratch clone built from the academic paper *TradingAgents: Multi-Agents LLM Financial Trading Framework* (arXiv [2412.20138](https://arxiv.org/abs/2412.20138)), on the native Anthropic SDK: ~10 agents argue each call, an independent risk agent can veto it. Separation of duties as design.
- **[Kalshi Calibration Study](./projects/06-kalshi-trading/)** — re-ran a published trading-strategy paper on the latest LLM across 1,274 markets to test whether a stronger LLM changed the result. It didn't; the markets are well-calibrated. The negative result is the finding.

---

## Stack

Python · TypeScript · FastAPI · async SQLAlchemy · PostgreSQL · Next.js / React. Claude as the primary model (Haiku for extraction, Sonnet for reasoning and agents); Grok and local models in the mix. Controls-grade hygiene: pytest, strict mypy, Docker, signed artifacts, CI gates, custom MCP servers and Claude skills. Finance plumbing through QuickBooks Online, Plaid, and Financial Modeling Prep.

The full parts list — connectors, skills, and orchestration — is in [`TOOLSTACK.md`](./TOOLSTACK.md).

---

## Contact

I'm open to conversations on AI-native finance systems, vertical agent implementations for private equity and asset management, finance transformation leadership roles, and advisory work.

[LinkedIn](https://www.linkedin.com/in/peter-c-hanselmann-cpa/) · phanselm315@gmail.com
