# Build Log & Full Project Index

The chronological record behind [Finance Engineering](./README.md) — every build, in order, kept for transparency. The README curates the work that matters most to institutional finance; this is the full cadence and the complete index, including the early foundations and the personal and nonprofit projects where the method got tested on real, messy data.

I started in March 2026 with basic Python and no API or agent experience, and built in public week over week. The early work is basic; it's kept visible so the progression is checkable.

---

## Roadmap

| Month | Focus | Milestone |
|-------|-------|-----------|
| 1 | **Foundation**: prompt engineering, first API calls, daily tools | First working API script + system prompt library |
| 2 | **Master the API**: CLI tools, PDF automation, scoring tools | 3 CLI tools in active use |
| 3 | **Tools & Agents**: web scraping, external APIs, data pipelines | Scraper-agent + parish bookkeeping system |
| 4 | **Real Products**: apps used by real people in real life | Family Flow App + Wacker Advisors OS + four-agent PE value-creation suite + Forge fund-accounting ERP |
| 5 | **Advanced Architecture**: multi-agent, ML training, trading systems | 007 paper-trading run · Kalshi calibration study · Sass Factory |
| 6 | **Deploy & Apply**: put the toolkit to work on real engagements | Capabilities deployed for portfolio companies and funds — as an advisor or in a finance-transformation role |

---

## Finance & PE Index

The work most directly tied to fund accounting, PE and asset-management operations, compliance, and trading.

| Project | What it is |
|---------|------------|
| [Forge — AI-Native Fund Accounting Platform](./projects/26-forge-fund-erp/) | From-scratch fund-administration platform with a replayable, attestation-backed accounting core that reproduces byte-identical. ASC 946 statements, distribution waterfalls, per-class LP reporting — built via gated Claude Code phases and adversarial multi-agent review. |
| [Value-Creation Suite](./projects/20-value-creation-suite/) | Four diagnostics for PE portfolio companies — working capital, freight, inventory, procurement — each a deterministic engine with a narrow LLM layer, each rolling a single-portco EBITDA bridge up to a fund-level play. Four public repos. |
| [Wacker Advisors OS](./projects/16-wacker-advisors-os/) | The operating layer for an AI-native fractional CFO + CCO practice: compliance calendars, deliverable tracking, document automation. |
| [007 Trading Agent](./projects/17-007-trading-agent/) | Multi-agent equities system: ~10 agents ingest data, debate each trade, clear it against an independent risk veto. |
| [Kalshi Calibration Study](./projects/06-kalshi-trading/) | Academic question → trading bot → research finding: BTC daily binaries are well-calibrated with no directional edge. A negative result, reported. |
| [Business Prompt Library](./projects/04-business-prompt-library/) | Claude skills in daily use for CFO/CCO advisory, SEC private-fund compliance, and ASC 946 investment-company accounting. |
| [Monthly Financials Builder](./projects/09-monthly-financials-builder/) | Python CLI that assembles the full monthly board financial package from raw QuickBooks Online exports in one command. In monthly use for a nonprofit board. |
| [Parish Bookkeeping System](./projects/11-parish-bookkeeping-system/) | Documented 30 years of undocumented month-end process and automated QuickBooks Online workflows across multiple entities — two churches, a school, and ministries. |

---

## Full Chronological Index

Every build, in order.

| #  | Project | Month | Description | Started |
|----|---------|-------|-------------|---------|
| 01 | [Tax Prep with Claude](./projects/01-tax-prep-with-claude/) | 2 | Used Claude alongside Free Tax USA to work through a full personal tax filing. First high-stakes real-world AI use. | Apr 2026 |
| 02 | First API Call | 1 | Node.js script making a live Claude API call. The foundational proof of concept. | Mar 9, 2026 |
| 03 | [Municipal Meeting Scanner](./projects/03-municipal-meeting-scanner/) | 1–2 | Node.js + Playwright + Claude API: scrapes ~20 gov websites weekly, extracts housing/zoning items into a formatted HTML report. | Mar 9, 2026 |
| 04 | [Business Prompt Library](./projects/04-business-prompt-library/) | 1–2 | 6 production Claude skills: CFO/CCO advisory, SEC compliance, investment accounting, email drafting, website copy, resume. | Mar 2026 |
| 05 | [Workforce Housing Analyzer](./projects/05-workforce-housing-analyzer/) | 2 | Iterative Excel + AI parcel analysis tool for a Leelanau County land acquisition campaign (v3 → v102+). | Mar 2026 |
| 06 | [Kalshi Trading](./projects/06-kalshi-trading/) | 2–3 | Academic paper → trading bot → research finding: a paper-trading cohort and a 1,274-market calibration study both showed Kalshi's BTC binaries are well-calibrated with no directional edge. | Apr 2, 2026 |
| 07 | [Obsidian Second Brain](./projects/07-obsidian-second-brain/) | 2–3 | Knowledge system on Obsidian: standardized capture templates feed Claude-assisted synthesis writing and densely linked maps of content. | Apr 13, 2026 |
| 08 | [Aether Advisors](./projects/08-aether-advisors/) | 2–3 | AI-powered marketing company build: AI image generation, marketing program design, brand strategy, SEO/GEO audits. | Apr 23, 2026 |
| 09 | [Monthly Financials Builder](./projects/09-monthly-financials-builder/) | 2–3 | Python CLI: auto-assembles board financial package from QBO exports. | Apr 23, 2026 |
| 10 | [Email Scoring Tool](./projects/04-business-prompt-library/) | 3 | Single-file HTML tool scoring AI-drafted community emails against strict brand voice rules. Folded into the Business Prompt Library page. | Apr 2026 |
| 11 | [Parish Bookkeeping System](./projects/11-parish-bookkeeping-system/) | 3 | Documenting 30-year undocumented processes, automating QBO workflows for 2 churches + school + ministries. | Apr 2026 |
| 12 | [Resume Builder Skill](./projects/04-business-prompt-library/) | 3 | Claude skill that ingests any job description and produces a tailored version of a formatted master resume. Folded into the Business Prompt Library page. | May 2, 2026 |
| 13 | [Public-Records Relationship Mapper](./projects/13-fraud-finder/) | 3 | Public-data pipeline linking Illinois contract awards, entity registrations, and political contributions; Claude scores which connections merit human review. | May 2, 2026 |
| 14 | [Claude Audit](./projects/14-claude-audit/) | 3 | Python script to audit and clean up a computer's file system using AI. | May 7, 2026 |
| 15 | [Family Flow App](./projects/15-family-flow-app/) | 3 | Personal app: shared calendar aggregation, grocery hidden-API integration, financial dashboard, Plaid. | Mar 2026 |
| 16 | [Wacker Advisors OS](./projects/16-wacker-advisors-os/) | 3 | Operating layer for a one-man outsourced CFO/CCO/COO firm. | Mar 2026 |
| 17 | [007 Trading Agent](./projects/17-007-trading-agent/) | 3–5 | Multi-agent equities trading system: a from-scratch clone of the "TradingAgents" framework (arXiv:2412.20138). ~10 agents debate the call and clear it against an independent risk veto; paper-trading runs began June 2026. | May 16, 2026 |
| 18 | Grok Brain Export | 3 | Export and clean Grok outputs and conversation history for structured integration into the Obsidian second brain. | May 2026 |
| 20 | [Working Capital Diagnostic](./projects/20-value-creation-suite/) | 3–4 | AR diagnostic + collections tool for PE portfolios with a human approval queue and fund-level treasury rollup. | May 22, 2026 |
| 21 | [Freight Carrier Optimization](./projects/20-value-creation-suite/) | 3–4 | Re-prices shipment history against live carrier rates and rolls a single-portco EBITDA bridge to a fund-level play. | May 22, 2026 |
| 22 | [Inventory Diagnostic](./projects/20-value-creation-suite/) | 3–4 | ABC × XYZ catalog segmentation, safety-stock and EOQ sizing, dead-SKU surfacing, fund-wide pooling play. | May 2026 |
| 23 | [Procurement Spend Diagnostic](./projects/20-value-creation-suite/) | 3–4 | Vendor-master cleanup, spend classification, tail/maverick/concentration risk, fund-wide negotiation playbook. | May 2026 |
| 24 | [Twitter Stock Research Pipeline](./projects/24-twitter-stock-research/) | 3–4 | Near-zero-touch pipeline from X bookmarks to a stock-research system: scheduled scrape + AI classification into Obsidian, a 500+-ticker tracker with weekday price refresh (FMP), and on-demand Claude valuation sessions. | May 17, 2026 |
| 25 | Taste Interview: Voice Profile | 3–4 | 100-question Claude-conducted interview extracting a personal writing voice into a profile any AI writing task can load. | May 28, 2026 |
| 26 | [Forge: AI-Native Fund Accounting Platform](./projects/26-forge-fund-erp/) | 4–5 | From-scratch AI-native fund administration platform: replayable, attestation-backed accounting core built via a two-tier Claude workflow (architect sessions → gated Claude Code phases → adversarial multi-agent review). | Jun 3, 2026 |
| 27 | [SBGC CLT — STORM Research Synthesis](./projects/27-sbgc-clt-storm/) | 3–4 | Test of Stanford's STORM / Co-STORM multi-perspective article generation over a built corpus, used to review a community group's community-land-trust research. Rebuild planned. | Jun 2026 |
| 28 | [Sass Factory](./projects/28-sass-factory/) | 5 | Gated software factory: spawns coding agents in isolated git clones, streams their work live, and gates every change at the merge boundary (deterministic `check-all` + an adversarial review agent that votes merge/block), proposing merges as PRs so nothing merges unchecked. The gated build-loop pattern generalized into a reusable system. | Jun 25, 2026 |

---

## Weekly Cadence

**Month 1 — Foundation (March 2026)**
- First live Claude API call (a six-line Node.js script); kicked off the Municipal Meeting Scanner the same session.
- Built the Business Prompt Library: six Claude skills (CFO/CCO advisory, SEC compliance, ASC 946 accounting, community email, website copy, resume). Lesson: a structured system prompt with hard rules beats a generic one decisively.

**Month 2 — Master the API (March–April 2026)**
- Municipal Meeting Scanner: Playwright pulls ~20 government sites into a scored housing/zoning report.
- Workforce Housing Analyzer: iterative AI parcel analysis (v102+); extracted county tax-parcel data in minutes versus a $2,500 quote.
- Kalshi Trading begins as an academic question and becomes a BTC paper-trading bot.
- Obsidian Second Brain matures from capture into a Claude-assisted synthesis workflow.
- Monthly Financials Builder and Aether Advisors launch the same day.
- Email scoring tool: first structured brand-voice scoring layer.
- Tax Prep with Claude: first high-stakes use — a full personal filing.

**Month 3 — Tools & Agents (May 2026)**
- Parish Bookkeeping: stepped in as interim bookkeeper; documented 30 years of undocumented process and automated QuickBooks workflows across multiple entities.
- Resume Builder skill and Claude Audit.
- Family Flow App: shared family calendar, unofficial grocery API integration, Plaid spending dashboard.
- Wacker Advisors OS: the operating layer for a one-person CFO/CCO practice.
- Kalshi: the edge didn't hold — a 1,274-market calibration study found no directional edge. The negative result is the finding.
- 007 Trading Agent: a from-scratch multi-agent equities system, ~20 hardening sprints into a paper-trading run.
- PortCo Value-Creation suite — working capital, freight, inventory, procurement — shipped as one body of work.
- Twitter Stock Research pipeline, Grok Brain Export, and the Taste Interview voice profile.

**Month 4 — Real Products (June 2026)**
- Forge: eleven gated phases in a few days; a replayable, byte-identical core. Then ASC 946 statements, distribution waterfalls, per-class LP reporting, and byte-exact seed surgery — ~580 tests with adversarial review green.
- Kalshi calibration study finalized.
- Wacker OS built out ahead of client work.

**Month 5 — Advanced Architecture (June 2026)**
- Sass Factory: the gated-loop pattern generalized into a reusable software factory — gated at the merge boundary, now driving its own (human-defined) backlog through its gates.

**Month 6 — Deploy & Apply**
- Underway: the repositioning above, outreach, and first paid work.
- Repositioned the portfolio's front matter to a "Finance Engineering" thesis — the top-level README now leads with the operating-model-first argument and three carrying builds.
- **Status sweep (Jul 3):** Forge came off "at rest" — the value-creation layer advanced with a further CI-green increment and a larger test suite. Sass Factory ran a full end-to-end self-advancing cycle and tightened its gate chain with a new check. The 007 paper-trading run is still live into early July. Obsidian's synthesis/structural-linking layer got another upgrade. Wacker OS runs the firm's own back office, with the public website in final design — still pre-launch, no client engagements yet. SBGC STORM unchanged. Repo housekeeping: recovered three project READMEs (Wacker OS, Twitter Stock Research, Forge) that a bad snapshot had truncated mid-file.
- **Status sweep (Jul 13):** Forge grew a web front end — a Next.js 15 / React 19 / TypeScript-strict / Tailwind app wired straight to the FastAPI attested core, already serving live ASC 946 statements, the waterfall, ingest tie-out/queue, and a value-creation demo with per-cell provenance color; the "command center" landing view was designed in Claude Design (Fable) and is being ported in by hand (working prototype). Two accounting increments also landed off the attested log: an ASC 946 / ASC 230 Statement of Cash Flows (read-only, anchor-neutral, tri-reviewed) and a portfolio-company chart-of-accounts v2 reseed. The Obsidian second brain gained a hosted layer — capture and intake now run on a VPS with an email-to-intake path (voice notes next) and the vault reachable from my phone; a vault MCP bridge is the next piece. The Workforce Housing Analyzer got a clean-slate rebuild in Claude Design that landed in a presentation-ready deliverable. 007's live paper-trading run continues into mid-July. Wacker OS unchanged — still pre-launch, no client engagements.

---

*Started: March 1, 2026 · Updated: July 13, 2026 · Inspired by [@cyrilXBT's roadmap](https://x.com/cyrilXBT).*
