# Portfolio-Company Value-Creation Suite

*Deliberately not agents: deterministic engines with the LLM only where language and
judgment are the point.*

**Status:** 🔄 Active  
**Started:** May 22, 2026  
**Repos:** four public repos, linked per diagnostic below  

## What This Is

Four operational-finance diagnostics for PE portfolio companies — working capital,
freight, inventory, and procurement — covering the cash conversion cycle and the largest
controllable cost lines in a portfolio. Each pairs a deterministic analytics engine with
a narrow LLM layer, produces a board-ready EBITDA bridge, and re-runs across the whole
fund so a single-portco win rolls up to a fund-level play.

All data is synthetic — one fictional fund (Hadrian Capital Partners) shared across all
four — but the input CSVs deliberately mirror what NetSuite, QuickBooks, or Sage export,
so pointing a diagnostic at a real company is a column-mapping exercise, not a rebuild.

## How the Suite Holds Together

- **Deterministic core, narrow LLM.** Every figure traces to an explicit calculation —
  auditable line by line. The model writes prose and judgment calls, never numbers.
- **Cross-diagnostic guardrails, written in.** Procurement owns vendor unit cost; freight
  owns shipping and logistics; working capital owns DSO; inventory owns DIO. The
  boundaries are explicit config constants, so nothing double-counts when all four run
  against the same fund.
- **Board language.** Output is an EBITDA bridge with downside / base / upside
  flow-through and enterprise value held at each company's entry multiple — no multiple
  expansion. Structured the way a deal team expects to receive it.
- **Reproducible by default.** Mock mode runs offline and byte-identical; real APIs are
  touched only when caches are explicitly rebuilt. Python; Streamlit apps and Jupyter
  walkthroughs share one `src/` per repo so the demo and the deep-dive can't drift apart.

## 1. Working Capital

**Repo:** [github.com/phanselm315/working-capital-agent](https://github.com/phanselm315/working-capital-agent)

The accounts-receivable analysis and collections workflow a turnaround consultant is
hired to do — in seconds, re-runnable across the portfolio. Three acts: a deterministic
diagnostic (DSO vs. target, aging curve, concentration, disputed exposure, triangulated
recoverable cash) with a Claude-written narrative; a remediation loop (rules-based
segmentation, a priority-ranked collector worklist, a tone-matched collection email per
account — warm for a strategic anchor, firm at 90 days, dispute-first where contested);
and a treasury rollup across the fund. An **approval queue** sits between the system and
the outside world: nothing sends until a person signs off.

## 2. Freight Carrier Optimization

**Repo:** [github.com/phanselm315/freight-carrier-optimization-agent](https://github.com/phanselm315/freight-carrier-optimization-agent)

Re-prices a manufacturer's twelve-month shipment history against live carrier rates —
parcel through EasyPost, LTL through Warp Freight — and decomposes savings lever by
lever: carrier mix, mode selection, consolidation, expedited-freight reduction. The
status-quo inefficiency premium, the single largest assumption, is one named, tunable
parameter, and real rates are flagged separately from modeled fallbacks. The LLM writes
exactly one thing: the carrier negotiation scorecard's talking points. The judgment here
is in finding the cost line — recognizing freight as the largest *controllable*, unmanaged
spend — not in the arithmetic that optimizes it. The fund rollup adds the lever no single
company has on its own: pooled carrier volume negotiated as one buyer across the
freight-intensive portcos, for a tiered discount (3 / 6 / 10% — light pooling, a base
programme, a fully consolidated bloc) layered on top of each company's standalone result —
value the fund captures that no mid-market company could command alone.

## 3. Inventory

**Repo:** [github.com/phanselm315/inventory-intelligence-agent](https://github.com/phanselm315/inventory-intelligence-agent)

Segments a distributor's catalog 3×3 by ABC × XYZ with per-cell service-level targets
(AX at 99%, CZ at 85%), sizes safety stock off the standard deviation of *forecast error
against a hold-out* — the forecast can lie to itself; the hold-out can't — plus
EOQ-rounded cycle stock, dead-SKU surfacing, and obsolescence reserve correction. The
fund rollup builds a canonical-SKU map across portcos and applies classical √N
safety-stock pooling, capped at 8% / 15% / 22% tiers reflecting what a real pooling
program lands, not what the math allows in a vacuum. The working-capital release is the
case: it shows up on the bank statement, not in a footnote.

## 4. Procurement Spend

**Repo:** [github.com/phanselm315/procurement-spend-intelligence-agent](https://github.com/phanselm315/procurement-spend-intelligence-agent)

Cleans the vendor master with a two-pass clusterer — exact match on a noise-stripped key,
then rapidfuzz `token_set_ratio`, with a numeric-token guard so two vendors with
different account IDs never merge on text similarity alone (precision ≥ 0.99, recall
≥ 0.96 against the seeded answer key — on synthetic data where the generator plants the
aliases; a ceiling, not field performance). Classifies spend into a 10-category taxonomy
and surfaces tail spend, maverick spend, and concentration risk; savings decompose into
four named levers, never one black-box percentage. The fund rollup builds a spend cube
(vendor × category × portco), scales portfolio leverage by the share of spend genuinely
contestable in 12–18 months (default 40%), and produces a category-by-category
negotiation playbook an operating partner can take into a kickoff meeting.

## Lessons Learned

The deterministic-vs-LLM boundary is a design decision, not an afterthought. Drawing it
explicitly — arithmetic stays deterministic, language goes to the model — is what makes
the output trustworthy to a finance reader who will check the numbers.

Suite-level guardrails matter as much as in-portco math. Once four diagnostics touch the
same fund, the question becomes who owns what dollar. Explicit boundaries are how the
suite stays additive instead of triple-counting.

A diagnostic is only half the job. The value is the standing process — re-run it on every
data refresh and a one-time consulting deck becomes an always-on workflow, a reusable
fund asset instead of slides.

---

*Part of [Finance Engineering](../../README.md)*
