# Office of the CFO Skill Suite + Agent Rollout

**Status:** 🔄 Active — ten skills in production, three in development; in use across a delivery team of about 45  
**Started:** August 2026  
**Code:** Built at my current firm, a PE-focused consulting firm, on client work. The code is the firm's, so this page stays high-level: no code, no client data, no internal names.

> A PE-backed company needs the same finance deliverables every month — statements, a 13-week cash forecast, debt and borrowing-base math, a board-package tie-out, a closing statement — and every consultant was rebuilding them in a spreadsheet the next reviewer had to re-derive before trusting.

## The Operating Problem

On a consulting bench, the same deliverables get rebuilt engagement after engagement. Each one carries judgment that lives in one person's head: which document wins when the credit agreement and the borrowing-base register disagree, what a covenant test actually counts, when a variance is a finding versus a rounding difference. When that judgment isn't written down, the work doesn't compound, and the reviewer can't tell a real number from a plausible one.

Handing the bench a model makes that worse, not better. A model will happily fill a missing term with a number that looks right, widen a tolerance until a check passes, and present a workbook in the same breath it built it.

## The Engineering Approach

Thirteen skills across four workflows, all on one philosophy: **judgment goes into a file a person reviews, and everything after that is deterministic, gated, and traceable to a source.**

| Workflow | What the skills cover |
| --- | --- |
| Financial statements | Trial balance to income statement, indirect cash flow, consolidation — thin skills over one shared statement library so layouts can't drift |
| Cash and liquidity | 13-week cash forecast that orchestrates a cash-data audit, the model workbook, and a cash flash memo; debt schedule; borrowing-base certificate (in development) |
| Board reporting | Board-package tie-out and variance drivers (both in development) |
| Transactions | Closing statement and NWC true-up |

Every production skill runs the same seven-stage pipeline, and only one stage uses judgment:

1. **Inventory the inputs.** A script opens every file and flags what silently corrupts output — uncached formulas, hidden rows inside totals, placeholders, figures in thousands, totals that don't foot.
2. **Stop on bad sources.** A source that doesn't tie ends the run before any mapping.
3. **Extract into a deal or config file** — the judgment stage. Every term is stored as `{value, reference, source, confidence}`, with confidence one of *doc*, *derived*, *assumed*, or *missing*. Conflicts are recorded with both values; gaps become open items with a severity.
4. **Review, then wait.** The review renders what changes the numbers first, and the turn ends. The build refuses to run if the deal file changed since the last review.
5. **Build deterministically.** A CLI builds the workbook. No workbook code is written by hand.
6. **Gate.** Recalculate headless, scan for errors, require every check at zero, and compare every figure to an independent engine within $0.01.
7. **Report** in a fixed order, written from the gate's JSON output, never from the console.

## Rolling It Out

The skills move up a status ladder — in development → shareable → team testing → agent-harness candidate → production — so nothing reaches a client engagement on the strength of a demo. Every deliverable is still reviewed by a professional before it reaches a client; the output is a starting point, not a sign-off.

The suite is now one piece of a wider firm platform I'm helping build. A model-agnostic agent harness runs the skills so the firm can switch to cheaper models without rewriting them; engagement hubs live in Notion; budgets and time entry sync from the firm's project-tracking system and its ERP. The data boundary is a design decision, not a setting: the firm's document store stays outside the agent harness, and material reaches the engagement hubs by a one-way copy. Next is a business-development tool with a lead engine feeding an internally built CRM, integrated with Teams, Outlook, and the calendar — then a command center where each person sees their engagements, budgets, and blockers.

## Key Decisions

- **The model never types a figure.** Every number is a pointer to a source cell, a cited page, a registered term, or a script's output. Typed estimates are rejected, and a missing value stays null and becomes an open item.
- **No plug, ever.** A difference over tolerance fails and stays visible. A non-zero check that's a real finding is cleared only by an explanation that says so — and tolerances are set at intake, before any result is seen.
- **Gates block; they don't remind.** A failing gate stops the workbook, the memo, and the client page. A check that couldn't run reports SKIPPED, never passed.
- **Findings go both ways.** On a closing statement, the review raises items that favor either side. A review that only finds money for its own client gets discounted by the other side.
- **Client specifics live in config, not in skills.** A client-specific forecast skill was retired; mappings, entities, and settings moved to per-client config outside the shared repo.

## Lessons Learned

Most of the rules exist because something broke. One board-reporting skill carries 29 numbered rules; each one is there because a model broke it in a blind test.

The model's failure modes were predictable once written down: it drifts toward plausible numbers, it widens tolerances to make checks pass, and it builds and presents in one breath. Each got a structural answer rather than a stern instruction — a citation check on every *doc*-confidence value, bands fixed before results exist, and a review stamp that makes sign-off a separate step.

A tie is not correctness. A zero difference in the indirect cash flow proves coverage and balance, not classification; a tie to the upstream package the source was built from proves coverage only.

The biggest risk in a multi-skill pipeline turned out to be routing, not math. "Roll the forecast" could load only the workbook skill and skip the data audit, the client config, and the covenant escalation. The fix was a description that says the workbook skill is normally called by the forecast, not a merge — and I only got there by reading the files. Judging two skills by their descriptions alone, I'd recommended merging them; the files showed two layers of one pipeline.

The honest gap: the debt-schedule skill feeds covenant numbers clients act on and shipped without a test suite. Its stress option tests a workbook, not the skill. The rule now is that every fix ships with a test that fails without it — the reason the closing-statement suite grew to 74 tests — and closing that gap on the debt schedule is the next piece of hygiene.

Test data leaks, too. A scan found real client workbooks in fixtures and client names in docstrings. Fixtures are now synthetic, built by generator scripts, and a client-name scan runs before every release.

## Related

- [AI-Native Consulting OS](../29-ai-native-consulting-os/) — the capability / steward / risk-tier design this rollout puts into practice
- [Forge](../26-forge-fund-erp/) — the same deterministic-core instinct applied to fund accounting
- [Portfolio-Company Value-Creation Suite](../20-value-creation-suite/) — deterministic engines with a narrow LLM layer, for portco diagnostics

---

*Part of [Finance Engineering](../../README.md)*
