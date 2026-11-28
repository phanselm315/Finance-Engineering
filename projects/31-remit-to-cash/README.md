# Remit-to-Cash

**Status:** 🔄 Active. v1 released (tag `v1.0`). The scanned-paper extension (OCR v2) was measured and blocked by its own release gate. A v3 round now passes every gate on dev; its fresh holdout has not run yet.  
**Started:** November 24, 2026  
**Code:** [github.com/phanselm315/Remit-to-Cash](https://github.com/phanselm315/Remit-to-Cash). All data is synthetic: no PHI, and no real payer, provider, patient, or client.

> A PE-backed physical therapy rollup buys clinics faster than it standardizes billing. Every month the CFO asks the same question: is the cash we were told we were paid actually in the bank, and where it isn't, why, and who owns the fix?

## The Operating Problem

Every clinic the rollup buys brings its own billing system, its own payers, its own cash process, and its own bank accounts. Posters match 835s and paper remittances to bank lines by hand. Recoupments get netted without anyone noticing. Unapplied cash sits in suspense. Denials get worked from payer portals with no ranking by dollars. Each of those habits hides a specific failure: a recoupment booked as an underpayment, a deposit assumed because a remit says it was paid, a therapy-threshold denial rebilled without review.

My background is private capital, not healthcare. I picked this problem on purpose. PE-backed PT rollups live with it, the pattern carries to other finance workflows, and it let me test my method outside my home domain.

## The Engineering Approach

I narrowed the build to one recurring decision, the daily cash-application call, because a narrow decision has a defensible right answer. That let me build the ground truth before any model ran.

| Step | Who does it | Control |
| --- | --- | --- |
| Parse 835 remittances | Deterministic parser | Balancing rules R1 to R4 at $0.00 tolerance |
| Read paper remittance PDFs | Claude Haiku, structured output | Every value cites a line and a quote on the page. Code checks the value sits inside the cited span. A missing value stays empty. A failed cite blocks the item |
| Read scanned remits | Tesseract OCR, then the same extractor | Words read below a confidence cutoff are masked and left blank. Code repairs known misreads before the cite check |
| Match remits to claims and to bank deposits | Deterministic rules, kept apart | An 835 payment never counts as proof of a deposit |
| Exceptions and dispositions | Rule table, EX01 to EX12 | The exception taxonomy is the human-review boundary. A rule miss defaults to REVIEW |
| Review narratives | Claude Sonnet | Written from the exception's facts only. A narrative with any number not in the facts is dropped |

AUTO_CLEAR happens only when the match is exact, every invariant holds, the deposit is matched, and nothing is flagged. Even then it means "proposed for posting." The system never posts cash, writes off a balance, adds a modifier, rebills, or contacts a payer. A person does.

The measurement comes first. The golden set has 48 cases in v1 (30 dev, 18 holdout, each on its own seed), with expected outputs derived by separate code that cannot import the pipeline. Six gates cover valid output, no false AUTO_CLEAR, every balancing violation surfaced, no value filled where the document has none, every deposit link real, and every model value cited. The holdout stays frozen and runs once on a release candidate. A separate verifier agent, given only the spec, a clean clone, and the saved outputs, reproduced the holdout scorecard without a model call.

I scoped and designed it with Claude and ChatGPT, then ran the build as a gated Claude Code orchestration. Claude Code wrote the code, the tests, and most of the documents. I set what the model could and could not do, chose the gates, and made every call they escalated to me. Each one is in the repo's decisions log.

## Results

All scores below are on a frozen synthetic benchmark. They say nothing about cash recovered, days in A/R, or production use.

| Run | Cases | Gates | False AUTO_CLEARs | Material exceptions caught | Exceptions (precision / recall) | Fields correct |
| --- | --- | --- | --- | --- | --- | --- |
| v1 holdout, single run | 18 | 6 pass, 0 fail | 0 | 2 of 2 | 22/23, 22/22 | 1,869 of 1,870 |
| OCR v2 holdout, single run | 27 | 3 pass, 3 fail | 0 | 1 of 1 | 24/149, 24/28 | 2,371 of 2,704 |

- **v1 (text-layer paper and 835s) is released** at tag `v1.0`. I started after work on November 24 and had it done and documented by 2:30 the next afternoon.
- **OCR v2 (scanned paper) is blocked by my own release gate.** It never produced a false AUTO_CLEAR, and every failure sent its item to a person. But most scanned errors are blanks, so most scanned items land in the review queue, and three gates fail.
- **v3 is in flight.** Four targeted fixes for the v2 holdout failures (misread claim IDs, blank amount columns, masked amounts, unreadable claim numbers), each with a regression test that fails before the fix. Every gate passes on dev. The fresh holdout runs once, on a separate approval.
- **Model spend for the whole build:** $7.35 over 1,986 calls, against a $20 cap enforced in code.

## Key Decisions

- **No accuracy targets.** The harness reports what it measures, misses included. A target invites tuning toward the number.
- **The model reads paper only.** 835s are structured data and go through a parser. The model works where reading is the hard part.
- **Rules decide, never the model.** Matching, balancing, and dispositions are code. The two rule readings that change cash outcomes were my calls: claims on a recoupment remit go to REVIEW, and a line that fails its balance also fails its claim.
- **A repaired ID must match exactly one ledger claim, or the item is blocked.** My addition to the v3 round. Code may fix an OCR misread, but it may not guess between two claims.
- **The version table is generated from scorecards, never typed,** and the release tool fails if the README drifts from them.

## Lessons Learned

A perfect dev score said more about the dev set than about the extractor. Every v1 version scored the same on dev, including a run with a larger model at many times the cost. The one holdout miss came from a layout dev never exercised: a watermark letter landed inside a printed amount, the model left it blank, and the item went to a person. My first diagnosis was wrong. The saved raw model response settled it in minutes, which is why every run keeps one.

The "same failure twice stops the phase" rule paid for itself. Blank OCR values crashed the core twice for the same reason. Instead of a third patch, I approved one sweep of every blank-value path, with a test that blanks each field in turn. It found failures no run had hit.

Synthetic scans let me choose how hard the test is. After the first dev runs I lowered the speckle noise and moved the OCR cutoff. I did both on dev only, before the v2 holdout was opened, and the repo reports the before and after next to the results.

The gates slowed me down more than once. Pushes, deletions, and holdout access all stopped until a decision was written down. They also kept a second holdout run from happening by accident.

What isn't built, stated plainly: underpayment against contracted rates (EX11), and human review itself (no reviewer, resolution log, or reason codes). The evaluation harness holds no healthcare logic, but I haven't built a second workflow on it, so the reuse is untested.

## Related

- [Office of the CFO Skill Suite](../30-office-of-the-cfo-skill-suite/): the same rule, judgment in a reviewed file and everything after it deterministic, applied to PE-backed company finance
- [Forge](../26-forge-fund-erp/): a deterministic core where a discrepancy is always a real signal

---

*Part of [Finance Engineering](../../README.md)*
