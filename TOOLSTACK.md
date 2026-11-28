# Tool Stack

The working inventory of what I build with. It's the operational companion to the one-paragraph **Stack** blurb in the [README](./README.md) — that's the pitch, this is the parts list. Kept current so the stack itself compounds instead of scattering across projects.

*Last updated: 2026-11-27*

---

## Models

- **Claude** — primary. Haiku for high-volume extraction and classification, Sonnet for reasoning, agents, and anything with judgment in the loop.
- **Grok** — secondary reasoning and cross-checks.
- **ChatGPT** — third opinion on design work. Used with Grok as an independent critique pair: two models review a design separately and the conflicts get reconciled before anything locks (how the [AI-Native Consulting OS](./projects/29-ai-native-consulting-os/) reached v2).
- **Local / open models** — in the mix for private or high-volume work that shouldn't leave the machine.

## Languages & Frameworks

- **Python** — engines, agents, data work.
- **TypeScript** — app and service layer.
- **FastAPI** + **async SQLAlchemy** — backend services.
- **Next.js / React** — front ends (Next.js 15 / React 19 on the Forge web app).
- **Claude Design (Fable)** — design and front-end generation: I design a view in Fable, then port it into the app by hand behind the type-check/lint gates. Used for the Forge command-center UI and a clean-slate rebuild of the Workforce Housing Analyzer.

## Data & Storage

- **PostgreSQL** — system of record for the deterministic cores.
- Local file-based context/memory stores — the persistent "brain" files that carry state between sessions (see [Wacker Advisors OS](./projects/16-wacker-advisors-os/)).
- **VPS host** — the [Obsidian second brain](./projects/07-obsidian-second-brain/)'s capture and intake jobs run hosted rather than laptop-bound, so ingest keeps running unattended and the vault is reachable from mobile. An email-to-intake path feeds it; a vault MCP bridge is next.

## Firm Platform — Office of the CFO Rollout

What I build on at my current firm, named by tool but not by internal system name (see [Office of the CFO Skill Suite](./projects/30-office-of-the-cfo-skill-suite/)).

- **Hermes** — the agent harness that runs the firm's skills, so the model can be swapped for a cheaper one without rewriting the method. Hermes is publicly available; the firm's instance is custom-built to spin up local instances on virtual desktops. Per-project versus per-person agent architecture, injected standard profiles, scheduled jobs (weekly dashboards), and a promotion path for a skill proven in Claude to move onto the harness.
- **Claude Enterprise Projects + Claude Docs** — team testing and shared context for skills on their way up the status ladder.
- **Claude Code** — build tool for the firm's command-center app.
- **Notion** — engagement hubs and the collaborative workspace.
- **Forecast** — budgets and time entry, feeding weekly engagement snapshots.
- **Microsoft Dynamics GP** — the firm's ERP, synced with project tracking.
- **SharePoint / Microsoft 365** — the document store, kept outside the agent harness by design; material reaches the engagement hubs by a one-way copy. The boundary is the control, not a setting.
- **Microsoft Teams + Outlook + calendar** — delivery channel for dashboards and integration points for the business-development tool.
- **Azure with role-based access** — hosting for the command center and the database behind an internally built CRM.
- **Zapier** — integration glue between the CRM, Notion, and the Microsoft stack.

## Finance & Market-Data Integrations (MCP connectors)

- **QuickBooks Online** — accounting (P&L, balance sheet, AR/AP aging, sales-by-customer/product), catalog, customers, payroll, invoicing, estimates, payment links, transaction import, benchmarking, cash flow. The finance plumbing.
- **Financial Modeling Prep** — quotes, financial statements, SEC filings, 13F, insider and congressional trades, DCF, technical indicators, earnings transcripts, economics, forex/crypto/commodity, analyst and TipRanks data, news. Market and fundamentals data.
- **Plaid** — bank and transaction connectivity (finance plumbing, per README).

## Productivity & Platform Connectors

- **Google Calendar** — event create/list/update, scheduling.
- **TurboTax** — tax interview, checklist, estimate, filing options, expert search.
- **Claude in Chrome** — DOM-aware browser automation for web apps without a dedicated connector.
- **Computer use** — native desktop control for cross-app workflows.

## Claude Skills

### Built by me

- `regpartner` — SEC private-funds compliance (Form ADV/PF, Marketing Rule, Custody Rule).
- `invcogaap` — ASC 946 investment-company accounting.
- `upwork-proposal` — feedback-updated proposal loop with a running lessons file.
- `website-copy` — brand-voice-compliant public content.
- `resume-builder` — tailored resume generation from any job description.
- `architect-journey-update` — status sweep of this portfolio repo.
- `session-status-handoff` — turns a build/session report into updated memory + a scoped resume prompt.
- `x-bookmarks-ingest` — routes X bookmarks into the Obsidian second brain.
- `wiki-ingest` — weekly/on-demand ingest of raw, Clippings, and intake into the vault's wiki layer with judgment rules baked in.
- `feedback-router` — routes a correction or lesson into the file that owns it, so a fix persists across sessions.
- `design-prompt-builder` — assembles a tailored Claude Design (Fable) redesign prompt from a brand/voice interview.

### Built at my current firm (described, not linked — the firm's IP)

Fourteen skills on one pipeline (inventory → stop on bad sources → extract to a reviewed file → build → gate → report):

- **Financial statements** — trial balance to income statement, indirect cash flow, consolidation, over a shared statement library.
- **Cash and liquidity** — 13-week cash forecast orchestrating a cash-data audit, the model workbook, and a cash flash memo; debt schedule; borrowing-base certificate (in development).
- **Board reporting** — board-package tie-out and variance drivers (in development).
- **Transactions** — closing statement and NWC true-up; opening balance sheet (in development).
- **Next** — cutoff testing first, then budget builder, quality of earnings, cross-system tie-out, payroll accrual.

### Stock (Anthropic)

- `meeting-prep` — research + prep briefs for any call or interview.
- `consolidate-memory` — merges duplicates and prunes stale facts across memory files.
- `schedule` — creates/updates scheduled tasks.
- `docx`, `xlsx`, `pptx`, `pdf` — professional deliverables.
- `skill-creator` — build, edit, and eval skills.
- `deep-research` — fan-out, verify, synthesize cited reports.
- `create-cowork-plugin`, `cowork-plugin-customizer` — plugin scaffolding and tailoring.
- `setup-cowork` — environment setup.

## Automation & Orchestration

- **Scheduled tasks** — recurring runs (bookmark sync, briefings, sweeps).
- **Custom MCP servers** — the encoded-judgment layer specific to my domains.
- **Cowork artifacts** — live, connector-backed HTML views that refresh on open.
- **Typeform → Airtable → Zapier → DocuSign → Google Drive** — the intake-to-signature automation chain behind Wacker Advisors OS (paused with the practice).

## Engineering Hygiene / Controls

- **pytest** — tests.
- **strict mypy** — typing discipline.
- **Docker** — reproducible environments.
- **Signed artifacts** — provenance on outputs.
- **CI gates** — nothing merges unproven.
- **Human-approval gates** — before any agent touches the outside world.
- **Frozen holdout + independent verifier.** The evaluation pattern from [Remit-to-Cash](./projects/31-remit-to-cash/): a golden set with expected outputs derived by code that cannot import the pipeline, a holdout run once per release candidate, a separate verifier agent that reproduces the scorecard from saved outputs, and a version table generated from scorecards, never typed.
- **Spend ledger with a hard cap.** Every model call priced into a ledger; a call that could cross the cap is refused before it is sent.
- **Tesseract OCR.** Scanned-remit ingest in Remit-to-Cash, with low-confidence words masked rather than guessed.
- **LibreOffice headless recalc + openpyxl** — the delivery gate for Excel workbooks: recalculate, scan for errors and `###`, require every check at zero, and compare each figure to an independent engine within $0.01.
- **Skill status ladder** — in development → shareable → team testing → agent-harness candidate → production. Nothing reaches a client engagement on the strength of a demo.
- **Skill release discipline** — versioned release zips with CHANGELOGs, a single check-all script before commit, regression fixtures with signed-off answer keys, and a rule that every fix ships with a test that fails without it.
- **Synthetic fixtures + client-name scan** — fixtures built by generator scripts, never real client workbooks; a deny-list scan for client names runs before release, passed at run time and never stored in a skill.
- **Control-honesty tags** — each control labeled `[platform]` (enforced by the system) or `[behavior]` (relies on the model following instructions), so no one mistakes a request for a guarantee.
- **Evidence labeling + task-level risk tiers** — the control pattern from the [AI-Native Consulting OS](./projects/29-ai-native-consulting-os/): every material assertion tagged `[sourced]/[derived]/[assumption]/[estimate]/[judgment]`, and every task tiered by its action and destination so ceremony matches blast radius. Portable to any build where a model drafts and a human owns the output.

---

## Maintenance protocol

This file is meant to be living. During any **Architect Journey status sweep** (the `architect-journey-update` skill), review this inventory alongside the project READMEs and add anything new: a connector I started using, a skill I built, a framework or model that entered the rotation. Update the *Last updated* date whenever it changes. New entries follow the existing grouping; if a genuinely new category appears, add a heading rather than forcing the item into an ill-fitting one.
