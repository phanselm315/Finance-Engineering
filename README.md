# Finance Engineering

I solve finance operating problems for private capital.

For fifteen years I've sat on both sides of the institutional table. I started in financial-services audit, then moved to the investor's seat and performed operational due diligence on roughly 75 hedge fund and private equity managers. Since then I've built and run the finance function from the inside: Northern Trust fund administration, an emerging lower middle market PE firm, and a long-standing internal PE investment program at Kirkland & Ellis. The work has been fund and portco accounting, controllership, compliance, and reporting: ASC 946 statements, ERP implementations, close processes, audit and custody readiness, distribution waterfalls, and LP reporting.

AI lets me encode those operating models into software. That is the only reason AI is in this repo. It is the newest implementation layer for work I've done my whole career.

Today I do that work at a PE-focused consulting firm, where I build the Office of the CFO skill suite our delivery team runs on. This is the public body of work behind it.

---

## Selected Work

Six builds carry the thesis. The first runs in production at my current firm, so I describe it rather than link it. The rest run on synthetic or anonymized data with production-style logic.

### [Office of the CFO Skill Suite + Agent Rollout](./projects/30-office-of-the-cfo-skill-suite/)

**Problem.** A founder-run company takes on its first private equity sponsor, and its finance team feels it first. The board package, lender covenants and a borrowing base, a 13-week cash forecast, the closing-statement true-up, and a deal team asking why a control works the way it does all arrive in the same few months. The team that has run finance for years knows the business better than anyone. What changes is who has to trust the numbers, and how hard they look. The work also reaches past board reporting: an opening balance sheet, cutoff testing, a budget the sponsor will hold the company to, and payroll accruals, since bonuses and commissions frequently aren't accrued.

**Approach.** Fourteen skills across four workflows, built at the firm where I work now. We used templates before. A template carries the format but not the decisions: the budgeting calls and the rulings from prior monthly reviews lived in people's heads and inboxes, not with the client's numbers. The skills hold that judgment in the context of each business, in one file a person reviews. Everything after that file is deterministic. Every term carries its source and an honest confidence (*doc, derived, assumed, missing*). The build won't run until the review is stamped. The workbook is recalculated, checked to zero, and compared figure by figure to an independent engine within $0.01. No plug, ever. A check that couldn't run reports SKIPPED, never passed.

**Result.** Ten skills in production and four in development, in use across a delivery team of about 45. Each skill climbs a status ladder from development through team testing to production. The suite now sits inside a wider firm platform I'm helping build: Hermes, a publicly available agent harness the firm runs as a custom build on virtual desktops; engagement hubs; and a data boundary that keeps the firm's document store out of the agent's reach by design. It is the one build here with a whole team depending on it.

### [Remit-to-Cash: Cash Application for a PE-Backed PT Rollup](./projects/31-remit-to-cash/)

**Problem.** A physical therapy rollup buys clinics faster than it standardizes billing. Each clinic brings its own billing system, payers, cash process, and bank accounts. Every month the CFO asks whether the cash the payers said they paid is actually in the bank, and where it isn't, why, and who owns the fix. Today posters match remits to bank lines by hand, recoupments get netted silently, and unapplied cash sits in suspense.

**Approach.** One decision, the daily cash-application call, built as a measured workflow. 835s go through a deterministic parser. The model reads paper remittances only, and every value it extracts cites its span on the page, which code checks. Matching, balancing at $0.00 tolerance, and dispositions are rules. A twelve-type exception taxonomy is the boundary where a person decides. The system never posts cash. A 48-case golden set, six gates, a frozen holdout run once, and an independent verifier that reproduced the holdout scorecard without a model call.

**Result.** v1 is released: on its single holdout run, all six gates passed, zero false AUTO_CLEARs, 22 of 22 exceptions caught, and 1,869 of 1,870 fields correct. The scanned-paper extension never produced a false AUTO_CLEAR either, but it failed three gates, so my own release gate blocked it. A v3 round with four targeted fixes now passes every gate on dev and waits on its one holdout run. Total model spend: $7.35 against a $20 cap. All data is synthetic, and the repo says so before it shows a number.

### [Forge: an AI-Native Operating Core for a PE Firm](./projects/26-forge-fund-erp/)

**Problem.** A PE firm runs on numbers that live in separate systems. Value-creation work happens at the portfolio companies, valuations get marked in a model, fund accounting sits in a fund-admin platform, and LP reporting (often supplemental reporting too) is stitched together by hand each quarter. Every handoff is a reconciliation, and no one can trace a figure in an LP statement back to the operating initiative that produced it.

**Approach.** One replayable, deterministic core that carries the whole chain. A value-creation initiative at a portfolio company drives dollars into that company's ledger. Those dollars re-mark its valuation in the model. The new valuation flows up through the fund's distribution waterfall, per-class LP economics, and ASC 946 statements into LP reporting. All of it is *derived* from one attested source, not reconciled into agreement. Nothing is hand-keyed twice, and every number traces back to the event that caused it.

**Result.** Five demo funds replay byte-identical from a signed event log. Every layer above it (valuations, waterfalls, ASC 946 statements, per-class LP economics) is *derived* from that one attested source, with 600+ tests behind it. The command center, live on main, shows the whole portfolio end to end: an initiative landing, the valuation it re-marks in the ledger, and that mark flowing up to the LP number, with each cell tagged attested, derived, or pending. I've migrated funds onto Allvue and Dynamo and worked inside the proprietary and point systems that carve this chain into pieces on the portco, deal, and fund-accounting sides. This is the platform I wanted in every one of those seats: one system from the deal-close model to exit, giving a GP's Office of the CFO a single view of a chain that used to live in a stack of spreadsheets.

### [Portfolio-Company Value-Creation Suite](./projects/20-value-creation-suite/)

**Problem.** Operational-finance diagnostics for portfolio companies die as slides at the end of an engagement. The work isn't reusable and never rolls up to the fund.

**Approach.** Four diagnostics, each pairing a deterministic engine with a narrow LLM judgment layer, each rolling a single-portco win up to a fund-level EBITDA bridge. Working Capital: AR and trapped cash, with collections outreach gated behind human approval. Freight: shipment history re-priced against live carrier rates, with fund-wide carrier-volume pooling. Inventory: ABC × XYZ segmentation, safety and cycle stock, fund-wide pooling. Procurement: spend classification, tail and maverick risk, a fund-wide negotiation playbook.

**Result.** The diagnostic becomes a reusable fund asset instead of a one-time deliverable. Code is public for all four.

### [Wacker Advisors OS](./projects/16-wacker-advisors-os/)

**Problem.** A one-person CFO/CCO practice has no back office. The person who wins and delivers the work also runs the compliance calendars, deliverable tracking, and recurring document work. When the revenue driver is also the entire administration, every new client adds a full load.

**Approach.** The firm's operating model made executable: compliance calendars, deliverable tracking, and document automation, with the recurring judgment encoded as rules and dedicated skills for SEC private-funds compliance and ASC 946 accounting. Every call I make is captured once and reused, so each decision makes the next one cheaper. A scheduled regulatory-update ingest pulls rule changes into the practice. I review and own all compliance output. The system accelerates the work and never makes the call.

**Result.** It ran the firm's own back office, from intake through engagement letter through invoicing, built ahead of the first client engagement. The practice is paused while I'm full-time at a consulting firm. The design stands as built.

### [AI-Native Consulting OS](./projects/29-ai-native-consulting-os/)

**Problem.** A consulting firm rolling out AI faces two questions that decide whether it helps or hurts. Does the value from an engagement compound, or does it evaporate when the engagement closes? Does client data stay where it belongs? Most rollouts hand people a prompt library and hope. A prompt library is model-specific, unowned, and quietly deskills the bench.

**Approach.** Encode the practice's operating model rather than its prompts. Three layers stay apart: a portable orientation kit a new hire clones, a centrally governed capability library that compounds and is never forked, and per-client engagement workspaces where all the real data stays. The unit is a *capability*: a versioned, stewarded method carrying its inputs, its human procedure, and its known failure modes. Three boundaries run through every task (environment, evidence, authority). Risk tiers match ceremony to blast radius. A two-minute close review turns each engagement into a scrubbed contribution that a steward, not the author, publishes. A coach mode asks a developing consultant for their own read before showing the firm's.

**Result.** Every control in it is a controls habit pointed at a new problem. The clean-room rule is an information barrier. Submit-then-publish is segregation of duties. The evidence labels are a tickmark legend. The tier table is an approval matrix. Design locked at v2 and stress-tested with a new-hire walkthrough; the worked fictional engagement runs the full loop, from a restricted-cash failure caught in a 13-week cash flow to the capability version it bumped. The kit itself hasn't been deployed. Its pattern has: the capability unit, the stewarded library, and the risk tiers now shape how the Office of the CFO skills above get built and promoted.

---

## In Production Use

Two earlier builds have real users today:

- **[Monthly Financials Builder](./projects/09-monthly-financials-builder/).** Turned a 45-minute monthly board-package assembly into a 10-second command. In monthly use by a nonprofit board.
- **[Parish Bookkeeping System](./projects/11-parish-bookkeeping-system/).** Documented 30 years of undocumented close process across multiple entities, automated the QuickBooks workflows, and handed the system off.

---

## What is Finance Engineering?

Finance transformation knows *why* a finance organization should work a certain way: where truth lives, what evidence an accounting event needs, how a close survives an audit. It usually stops at the slide deck. Software engineering can build the system but doesn't carry the operating model. A finance engineer does both. I design the operating model **and** encode it into software: the rules, the controls, and the "we don't book it until X" that normally live in a senior controller's head, made executable, replayable, and auditable. The model (Claude, Grok, ChatGPT) is rented and getting cheaper. The durable asset is the encoded judgment, the checks, and the audit trail around it, the layer institutional finance has always cared about most.

## How I Build

I start with the operating model. Why does this process exist? Where does the truth live? What evidence and approvals does the event need? Software comes last, and only for the parts that earn it. Output has to be verifiable and hard to degrade silently: gates inside gates, human approval before any agent touches the outside world, and replayable cores where a discrepancy is always a real signal. I learned that habit in audit and controllership, long before AI.

Every build, including earlier and personal projects, is in [`projects/`](./projects/). The chronological record is in [`LOG.md`](./LOG.md).

---

## Additional Research

Adjacent work. Good builds, but supporting evidence rather than the main thesis.

- **[Sass Factory: a Gated Software Factory](./projects/28-sass-factory/).** A build loop where nothing merges until it's proven. Coding agents work in isolated git clones, and every change is gated at the merge boundary by deterministic checks plus an adversarial review agent. The separation of duties from a finance close, applied to a machine that writes code.
- **[007: Multi-Agent Equities Research](./projects/17-007-trading-agent/).** A from-scratch clone of the academic paper *TradingAgents: Multi-Agents LLM Financial Trading Framework* (arXiv [2412.20138](https://arxiv.org/abs/2412.20138)), built on the native Anthropic SDK. About 10 agents argue each call, and an independent risk agent can veto it.
- **[Kalshi Calibration Study](./projects/06-kalshi-trading/).** I re-ran a published trading-strategy paper on the latest LLM across 1,274 markets to test whether a stronger model changed the result. It didn't. The markets are well calibrated, and I report the negative result as the finding.

---

## Stack

Python · TypeScript · FastAPI · async SQLAlchemy · PostgreSQL · Next.js / React. Claude as the primary model (Haiku for extraction, Sonnet for reasoning and agents), with Grok and local models in the mix. Controls hygiene: pytest, strict mypy, Docker, signed artifacts, CI gates, custom MCP servers, and Claude skills. For Excel deliverables: headless recalculation, checks that must read zero, and an independent engine every figure is compared against. Finance plumbing through QuickBooks Online, Plaid, and Financial Modeling Prep.

The full parts list (connectors, skills, orchestration) is in [`TOOLSTACK.md`](./TOOLSTACK.md).

---

## Contact

I'm open to conversations on AI-native finance systems, vertical agent implementations for private equity and asset management, finance transformation leadership roles, and advisory work.

[LinkedIn](https://www.linkedin.com/in/peter-c-hanselmann-cpa/) · phanselm315@gmail.com
