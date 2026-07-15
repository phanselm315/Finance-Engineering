# Tool Stack

The working inventory of what I build with. It's the operational companion to the one-paragraph **Stack** blurb in the [README](./README.md) — that's the pitch, this is the parts list. Kept current so the stack itself compounds instead of scattering across projects.

*Last updated: 2026-07-15*

---

## Models

- **Claude** — primary. Haiku for high-volume extraction and classification, Sonnet for reasoning, agents, and anything with judgment in the loop.
- **Grok** — secondary reasoning and cross-checks.
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
- **Typeform → Airtable → Zapier → DocuSign → Google Drive** — the intake-to-signature automation chain behind Wacker Advisors OS.

## Engineering Hygiene / Controls

- **pytest** — tests.
- **strict mypy** — typing discipline.
- **Docker** — reproducible environments.
- **Signed artifacts** — provenance on outputs.
- **CI gates** — nothing merges unproven.
- **Human-approval gates** — before any agent touches the outside world.

---

## Maintenance protocol

This file is meant to be living. During any **Architect Journey status sweep** (the `architect-journey-update` skill), review this inventory alongside the project READMEs and add anything new: a connector I started using, a skill I built, a framework or model that entered the rotation. Update the *Last updated* date whenever it changes. New entries follow the existing grouping; if a genuinely new category appears, add a heading rather than forcing the item into an ill-fitting one.
