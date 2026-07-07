# Wacker Advisors OS

**Status:** 🔄 Active — runs the firm's back office; no client engagements yet  
**Started:** Mar 2026  

## What This Is

The operating layer for a one-man outsourced CFO/CCO/COO advisory firm serving emerging
fund managers. Every workflow automated or AI-assisted: client onboarding, compliance
calendar management, deliverable tracking, invoice generation, engagement letters, and
quarterly reports. It runs the firm's own back office today, built ahead of the first
client engagement.

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
- `regpartner` — SEC compliance research (Form ADV, Form PF, Marketing Rule, Custody Rule)
- `invcogaap` — ASC 946 investment company accounting
- `website-copy` — brand voice-compliant public content
- `resume-builder` — tailored resume generation

**Design principle:** Zero-touch where possible, one-touch for exceptions. I review
and approve; the system executes. All compliance output is reviewed and owned by me as
the responsible professional — the skills accelerate, they don't decide.

## The Compounding Layer

The automation is the visible part, but it isn't the point. The point is that the firm's
knowledge compounds instead of evaporating. In a normal advisory practice the hard-won
judgment — how a particular client's compliance calendar really works, why an engagement
letter is worded the way it is, what went wrong last quarter and how it was fixed — lives
in one operator's head and dies at the end of each engagement. Here it lives in persistent
context and memory files the system reads at the start of every session and writes back
to at the end. Every correction, decision, and finished deliverable feeds back into the
files, so the next session starts smarter than the last. The skills run the same loop:
`upwork-proposal` keeps a running lessons file so each edited proposal sharpens the next
draft, and a feedback log captures anything corrected mid-session.

One caveat: it only compounds if the write-back discipline holds. Memory that isn't fed
goes stale and, worse, confidently wrong — which is why memory hygiene is a first-class
chore here (the `consolidate-memory` pass merges duplicates and prunes stale facts), not
an afterthought.

## Key Decisions

**Build the operating layer before the client load.** Infrastructure built under pressure
gets built wrong. Every workflow, document, and automation is designed at full quality
before the first client signs, so the first engagement runs on a tested system, not a
prototype.

**Persistent context files over re-explaining every session.** Every Claude skill reads
current business state from context files at session start. A new session doesn't require
re-establishing context — the AI already knows the business, the client roster, the
current OKRs, and the active constraints.

**"I" not "we" throughout all client-facing materials.** Solo practitioner reality is a
competitive advantage: clients get the principal directly, always. No hand-offs to
associates. The marketing and documents reflect this explicitly.

**Compliance calendar as the backbone.** For fund manager clients, missing a regulatory
deadline is catastrophic. The compliance calendar is automated with 60-day advance
alerts — with the calendar itself reviewed manually each month, because an automation
guarding against catastrophic failure needs its own control — and it is the first thing
built for every new client engagement.

## Current Milestone

Repositioned May 28, 2026: the firm is an AI-native fractional CFO + CCO practice
aimed at emerging fund managers and family offices, independent sponsors and search
funds, PE/VC portfolio companies, and owner-operated private businesses. The v2 website
shell reflecting the new positioning was built June 1.

As of early July: the OS runs the firm's own operations — intake through engagement
letter through invoicing — and the public website is in final design ahead of launch.
No client engagements yet; that's the next milestone, and this page will say so plainly
when it changes.

## Lessons Learned

The highest-leverage investment in a one-person firm is the operating layer — not the
work product. Well-structured systems mean each additional client adds less marginal
time than the last. Poorly structured systems mean each client adds a full linear load.

Building the skills first, before client pressure created shortcuts, produced a
significantly better result.

---

*Part of [Finance Engineering](../../README.md)*
