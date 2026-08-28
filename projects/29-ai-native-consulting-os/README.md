# AI-Native Consulting OS

**Status:** 🔄 Active — v2 design locked and stress-tested with a new-hire walkthrough; pre-deployment  
**Started:** August 9, 2026  
**Code:** Private build — kept high-level here; written against a hypothetical firm  

## What This Is

An operating system for how a consultant uses AI day to day, built for an Office of the
CFO / value-creation practice. It is a portable kit a new hire can clone and run on their
first engagement — not a prompt library and not a deck.

It answers the two questions that decide whether AI helps a consulting firm or hurts it.
**Does the value from an engagement compound, or does it evaporate when the engagement
closes?** And **does client data stay where it belongs?**

The premise: the deck is not what compounds. What compounds is the method underneath it and
the judgment riding on top — the call the firm has already made a hundred times, the way a
good add-back gets defended, the failure you only catch because someone got burned on it
once. The system captures that, tests it, and hands it to the next person.

## Architecture

**Three layers, deliberately kept apart.**

1. **Portable orientation kit** — scrubbed, holds zero client data. Teaches the whole system
   in one page, ships an always-on operator policy, and carries a fully fictional worked
   engagement so a new hire can walk the loop end to end before running their own.
2. **Firm capability repository** — the centrally governed library where reusable methods
   compound. Never forked, never written to directly. Two capabilities ship built
   (13-week cash flow, quality of earnings); the rest of the practice map is seeded as
   `draft` and fills in as engagements produce it.
3. **Engagement workspaces** — one per client, inside the firm's approved AI environment,
   holding all the real data. Cloned from a template.

**The unit is a capability, not a prompt.** A capability is the firm's tested method for an
outcome — versioned, owned by a named steward, carrying its inputs, its human procedure, its
known failure modes, and a worked example. Prompts age out with the model; the capability
survives it.

**Three boundaries, enforced as behavior in the operator policy.**
*Environment* — confidential material is processed only inside the approved environment and
leaves by exactly two doors: an approved client-delivery path, or the approved
sanitize-and-publish path into the library. *Evidence* — the model is never the authoritative
number; every material assertion is labeled `[sourced] [derived] [assumption] [estimate]
[judgment]` and traces to a source a human can open, and a missing input is left blank, given
as a range, or asked about — never invented. *Authority* — the model drafts freely and stops
for the review its risk tier requires.

**Risk tiers matched to blast radius.** Every *task* takes its own tier from its action and
destination — mechanical and reversible (0), analytical draft (1), decision support (2),
external or system action (3) — and escalates on its own merits. A task never inherits a
lower tier from the engagement default: a Tier-1 engagement still contains a Tier-3 lender
submission.

**The clean-room rule.** Material from one client's workspace never moves to another's.
Reuse always begins from an approved library capability: `Client A → sanitize + review →
Library → Client B`, never `A → B`.

**The compounding loop.** At each milestone the engagement runs a two-minute close review:
the model assembles what got more reliable, drafts the scrubbed candidate, fills the scrub
table, and produces a reliability receipt and a four-field contribution record. The
consultant *submits*; a steward and an independent reviewer *publish*. Segregation of
duties, borrowed straight from a close.

**Coach mode.** On a developing consultant's engagement, the system withholds the firm's
accumulated judgment and asks for *their* read first, logs it privately, then reveals the
capability and walks the difference. When many analysts miss the same call, that routes to
the steward as a teaching defect in the capability — never as a grade on a person.

## Key Decisions

**Version the method, not the prompt.** Prompt libraries are the standard AI-enablement
artifact and they rot: they are model-specific, unowned, and unfalsifiable. A capability has
a steward, a version, a `last_verified` date, and a list of failure modes that explain why
the version bumped. That is an auditable asset; a prompt folder is not.

**Contributors submit, stewards publish.** The single most likely failure of a shared
library is that everyone forks their own copy. So nobody writes to the library directly, and
the steward map carries a publication SLA — because if submissions dead-letter, consultants
route around the repository and the compounding dies. The map is a launch prerequisite, not
documentation.

**The safety is in the architecture, not bolted on.** Data enters at the workspace and stays
there; the model drafts, it never decides and never leaves the sandbox; a one-way door means
stop and ask. Promotion to the library is itself a Tier-3 action with an independent
re-identification review by someone who isn't the author.

**Label controls honestly.** Every control is tagged `[behavior]` (people and the model
follow it), `[platform]` (technically enforced and validated), or `[roadmap]` (intended, not
yet enforced). The kit is training-only until an accountable owner signs off on retention,
isolation, access control, logging, connectors, export controls, and audit trail. Calling a
behavior an enforced control is the lie that gets a firm in trouble, so the kit refuses to
tell it about itself.

**Coach mode is the point, not a feature.** Most AI enablement quietly deskills the bench: if
you always inherit the answer pre-digested, you never build your own judgment. Automating the
*settled* calls and spending the reps on the *unsettled* ones is what moves judgment up the
stack instead of hollowing it out.

## Current Milestone

Design locked at v2 — reconciled across two independent model critiques, then stress-tested
with a simulated new-hire walkthrough that produced eight fixes now folded into the scaffold.
The kit runs: orientation, operator policy, two built capabilities, engagement-room templates,
the close review, and a fully worked fictional engagement (a 13-week cash flow where a
restricted-cash failure gets caught, scrubbed, and fed back to bump the capability to v1.3).

Next is the part that matters — running it on one real engagement to see whether the close
review actually survives contact with a deadline.

## Lessons Learned

Everything here is a controls habit pointed at a new problem. The clean-room rule is
information-barrier discipline. Submit-then-publish is segregation of duties. The evidence
labels are a tickmark legend. The tier table is an approval matrix. None of it is novel to
AI — which is the argument: the firms that get this right will be the ones that already know
how to run a control environment, not the ones with the best prompts.

The hardest design problem wasn't the boundaries. It was making the compounding step cost
almost nothing. A contribution flow that takes twenty minutes at the end of an exhausting
engagement will not be run, and a library nobody feeds is worse than no library — it teaches
new hires that the system is a black hole. So the close review had to be two minutes of human
review over a machine-assembled draft, and "nothing reusable emerged" had to be a valid,
recordable outcome. A receipt that says nothing changed beats a manufactured junk primitive.

---

*Part of [Finance Engineering](../../README.md)*
