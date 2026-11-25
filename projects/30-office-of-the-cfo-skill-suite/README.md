# Office of the CFO Skill Suite + Agent Rollout

**Status:** 🔄 Active. Ten skills in production, four in development; in use across a delivery team of about 45.  
**Started:** August 2026  
**Code:** Built at my current firm, a PE-focused consulting firm. The firm has cleared me to discuss the skills; there is no client data here, and the code stays with the firm.

> A founder-run company takes on its first private equity sponsor. The finance team that has run the business for years now has to produce, and defend, a reporting package for an investor, a lender, and an auditor at once.

## The Operating Problem

The customer is the founder-run company in its first year with a sponsor. The deal closes and the asks start the same month: a board package the sponsor reads line by line, lender covenants and a borrowing-base certificate, a 13-week cash forecast, the closing-statement true-up, and a deal team asking why a control works the way it does. The finance team knows the business better than anyone who just arrived. What changes is who has to trust the numbers, and how hard they look.

The work also runs past board reporting. A new owner needs an opening balance sheet. The purchase price settles through a closing statement. Cutoff testing has to show revenue and costs landed in the right period. The company needs a budget the sponsor will hold it to. Payroll accruals need a fresh look, because bonuses and commissions frequently aren't accrued.

## What Was Missing

We worked from templates before. A template carries the format, not the decisions. The budgeting calls and the rulings from prior monthly reviews lived in people's heads and inboxes, not with the client's numbers. Each month the work started from a clean template and the same questions got asked again.

The skills hold that judgment in the context of each business. A decision made in one month's review is recorded once, with its source, and the next month starts from it.

A model alone would not fix this. Left to itself, a model fills a missing term with a number that looks right, widens a tolerance until a check passes, and presents a workbook in the same breath it built it. For a company under new scrutiny, one plausible wrong number in an early board package costs the sponsor's trust.

## The Engineering Approach

Fourteen skills on one rule: **judgment goes into a file a person reviews, and everything after that file is deterministic, gated, and traceable to a source.**

| Workflow | What the skills cover |
| --- | --- |
| Financial statements | Trial balance to income statement, indirect cash flow, consolidation. Thin skills over one shared statement library so layouts can't drift |
| Cash and liquidity | 13-week cash forecast, which runs a cash-data audit, the model workbook, and a cash flash memo; debt schedule; borrowing-base certificate (in development) |
| Board reporting | Board-package tie-out and variance drivers (both in development) |
| Transactions | Closing statement and NWC true-up; opening balance sheet (in development) |
| Next | Cutoff testing, then budget builder and payroll accrual |

Every production skill runs the same seven stages, and only one stage uses judgment:

1. **Inventory the inputs.** A script opens every file and flags what silently corrupts output: uncached formulas, hidden rows inside totals, placeholders, figures in thousands, totals that don't foot.
2. **Stop on bad sources.** A source that doesn't tie ends the run before any mapping.
3. **Extract into a deal or config file.** This is the judgment stage. Every term is stored as `{value, reference, source, confidence}`, with confidence one of *doc*, *derived*, *assumed*, or *missing*. Conflicts keep both values. Gaps become open items with a severity.
4. **Review, then wait.** The review shows what changes the numbers first, and the turn ends. The build refuses to run if the deal file changed since the last review.
5. **Build deterministically.** A CLI builds the workbook. No one writes workbook code by hand.
6. **Gate.** Recalculate headless, scan for errors, require every check at zero, and compare every figure to an independent engine within $0.01.
7. **Report** in a fixed order, written from the gate's JSON output, never from the console.

## Rolling It Out

Each skill climbs a status ladder: in development, shareable, team testing, agent-harness candidate, production. Nothing reaches a client engagement on the strength of a demo. A professional reviews every deliverable before it reaches the client. The output is a starting point, not a sign-off.

The suite is one piece of a wider firm platform I'm helping build. Hermes, a publicly available agent harness, runs the skills so the firm can move to cheaper models without rewriting them. Our instance is custom-built to spin up local instances on virtual desktops. Engagement hubs live in Notion, with budgets and time synced from the firm's project-tracking system and its ERP. The data boundary is a design decision: the firm's document store stays outside the agent harness, and material reaches the engagement hubs by a one-way copy. Next is a business-development tool with a lead engine feeding an internally built CRM, connected to Teams, Outlook, and the calendar. After that, a command center where each person sees their engagements, budgets, and blockers.

## Key Decisions

- **The model never types a figure.** Every number points to a source cell, a cited page, a registered term, or a script's output. Typed estimates are rejected. A missing value stays null and becomes an open item.
- **No plug, ever.** A difference over tolerance fails and stays visible. A non-zero check that is a real finding clears only with an explanation that says so. Tolerances are set at intake, before any result is seen.
- **Gates block delivery.** A failing gate stops the workbook, the memo, and the client page. A check that couldn't run reports SKIPPED, never passed.
- **Findings go both ways.** On a closing statement, the review raises items that favor either side. A review that only finds money for its own client gets discounted by the other side.
- **Client specifics live in config.** A client-specific forecast skill was retired. Mappings, entities, and settings moved to per-client config outside the shared repo.

## Lessons Learned

Most of the rules exist because something broke. One board-reporting skill carries 29 numbered rules, and each one is there because a model broke it in a blind test.

The model's failure modes were predictable once written down. It drifts toward plausible numbers, widens tolerances to make checks pass, and builds and presents in one breath. Each got a structural answer rather than a stern instruction: a citation check on every *doc*-confidence value, tolerance bands fixed before results exist, and a review stamp that makes sign-off a separate step.

A tie does not prove correctness. A zero difference in the indirect cash flow proves coverage and balance, not classification. A tie to the upstream package the source was built from proves coverage only.

The biggest risk in a multi-skill pipeline turned out to be routing. "Roll the forecast" could load only the workbook skill and skip the data audit, the client config, and the covenant escalation. The fix was a description saying the workbook skill is normally called by the forecast. I only got there by reading the files. Judging two skills by their descriptions alone, I had recommended merging them; the files showed two layers of one pipeline.

The honest gap: the debt-schedule skill feeds covenant numbers clients act on, and it shipped without a test suite. Its stress option tests a workbook, not the skill. The rule now is that every fix ships with a test that fails without it, which is why the closing-statement suite has 74 tests. Closing that gap on the debt schedule is the next piece of hygiene.

Test data leaks, too. A scan found real client workbooks in fixtures and client names in docstrings. Fixtures are now synthetic, built by generator scripts, and a client-name scan runs before every release.

## Related

- [AI-Native Consulting OS](../29-ai-native-consulting-os/): the capability, steward, and risk-tier design this rollout puts into practice
- [Forge](../26-forge-fund-erp/): the same deterministic-core habit applied to fund accounting
- [Portfolio-Company Value-Creation Suite](../20-value-creation-suite/): deterministic engines with a narrow LLM layer, for portco diagnostics

---

*Part of [Finance Engineering](../../README.md)*
