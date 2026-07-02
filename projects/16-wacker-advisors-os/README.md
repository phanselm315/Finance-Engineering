# Wacker Advisors OS

**Status:** 🔄 Active  
**Started:** Mar 2026  

## What This Is

Full AI-powered operating system for a one-man outsourced CFO/CCO/COO advisory firm
serving emerging fund managers. Every workflow automated or AI-assisted: client onboarding,
compliance calendar management, deliverable tracking, invoice generation, engagement
letters, and quarterly reports. Infrastructure is production-ready.

## Architecture

- **Automation stack:** Typeform → Airtable → Zapier → DocuSign → Google Drive
- **AI layer:** Claude skills for every document type and advisory function
- **Document suite:** NDA, Service Agreement, Named Officer Addendum — pre-filled from
  intake data, DocuSign-ready
- **Compliance layer:** Regulatory deadline tracking, Form ADV reminders, SEC filing
  calendar
- **Financial layer:** QuickBooks Online integration, automated invoicing on 1st of month

**Claude skills deployed:**
- Root `CLAUDE.md` operating layer — full COO/CFO operations with persistent context
  files, auto-loaded every session (replaced the `pch-advisory` master skill May 2026
  after skills proved to under-trigger)
- `regpartner` — SEC compliance expert (Form ADV, Form PF, Marketing Rule, Custody Rule)
- `invcogaap` — ASC 946 investment company accounting
- `website-copy` — brand voice-compliant public content
- `resume-builder` — tailored resume generation

**Design principle:** Zero-touch where possible, one-touch for exceptions. Peter reviews
and approves; the system executes.

## The Compounding Layer — the brain

The automation is the visible part, but it isn't the point. The point is that the firm's
knowledge compounds instead of evaporating. In a normal advisory practice the hard-won
judgment — how a particular client's compliance calendar really works, why we word an
engagement letter the way we do, what went wrong last quarter and how we fixed it — lives
in one operator's head and dies at the end of each engagement. Here it lives in persistent
context and memory files: a **brain** the system reads at the start of every session and
writes back to at the end.

That read-then-write loop is what makes the practice compound. Every session starts already
knowing the business state, the client roster, the active OKRs, and the current
constraints, so no time is spent re-establishing context. Every correction, decision, and
finished deliverable feeds back into the files, so the next session starts smarter than the
last. The skills themselves run the same loop: `upwork-proposal` keeps a running lessons
file so each edited proposal sharpens the next draft, and a feedback log captures anything
that got corrected mid-session. Knowledge earned once is reused indefinitely.

This is the firm-scale version of the thesis behind the whole repo — **institutional memory
as software.** The model is rented and commoditizing; the durable asset is the accumulated,
owned judgment layer around it. It's also why each additional client adds less marginal
effort than the last: the work isn't re-derived, it's inherited from the brain.

The honest caveat: it only compounds if the write-back discipline holds. A brain that isn't
fed goes stale and, worse, confidently wrong — which is exactly why memory hygiene is a
first-class chore here (the `consolidate-memory` pass exists to merge duplicates and prune
stale facts), not an afterthought.

## Key Decisions

**Build the OS before the client load.** Infrastructure built under pressure gets built
wrong. Every workflow, document, and automation is designed at full quality before the
first client signs. The first engagement runs on a production system, not a prototype.

**Persistent context files over re-explaining every session.** Every Claude skill reads
current business state from context files at session start. This means a new session
doesn't require re-establishing context — the AI already knows the business, the client
roster, the current OKRs, and the active constraints.

**"I" not "we" throughout all client-facing materials.** Solo practitioner reality is a
competitive advantage: clients get the principal directly, always. No hand-offs to
associates. The marketing and documents reflect this explicitly.

**Compliance calendar as the backbone.** For fund manager clients, missing a regulatory
deadline is catastrophic. The compliance calendar is automated with 60-day advance
alerts and is the first thing built for every new client engagement.

## Current Milestone

Repositioned May 28, 2026: the firm is now an AI-native fractional CFO + CCO practice
serving four client profiles — emerging fund managers and family offices, independent
sponsors and search funds, PE/VC portfolio companies, and owner-operated private
businesses. The v2 website shell reflecting the new positioning was built June 1.

As of late June, the OS is no longer just infrastructure-in-waiting — I'm running it on
live consultancy work, with the website launch impending. The system is proving itself on
real engagements rather than rehearsals.

## Lessons Learned

The highest-leverage investment in a one-person firm is the operating system — not the
work product. Well-structured systems mean each additional client adds less marginal
time than the last. Poorly structured systems mean each client adds a full linear load.

Building the skills first, before client pressure created shortcuts, produced a
significantly better result. The discipline to build the right foundation before
generating revenue is the difference between a practice that compounds and a busy job.

---

*Part of the [AI Architect Journey](../../README.md)*
