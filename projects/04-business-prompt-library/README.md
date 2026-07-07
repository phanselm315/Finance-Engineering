# Business Prompt Library

**Status:** ✅ Done  
**Started:** Mar 2026  

## What This Is

Six Claude skills in daily use covering CFO/CCO advisory, SEC compliance, investment
company accounting, community email drafting, website copy, and resume building. All
deployed and in active use in Cowork. This page also covers the two builds that grew out
of the library: the brand-voice scoring tool and the resume skill.

## Architecture

Each skill is a structured system prompt with:
- A defined role and operating context
- Hard rules the model cannot override
- Reference file pointers for persistent context
- Session start/close protocols for stateful work
- Output format standards

**Skills built:**
- `pch-advisory` — CFO/COO advisory operations for Wacker Advisors LLC
- `regpartner` — SEC private fund compliance (Form ADV, Form PF, Marketing Rule, Custody Rule)
- `invcogaap` — ASC 946 investment company accounting
- `sbgc-email` — Community email drafting with strict brand voice enforcement
- `website-copy` — Wacker Advisors public-facing content
- `resume-builder` — Tailored resume generation from job descriptions

All compliance output is reviewed and owned by me — the skills accelerate, they don't
decide.

## Key Decisions

**Hard rules over soft instructions.** Early prompts used language like "try to" and
"generally." Skills in real use need "never," "always," and explicit flags for when the
model must stop and ask. The difference in output consistency is significant.

**Context files over long prompts.** Each skill reads external files at session start
rather than embedding all context in the prompt itself. This keeps prompts maintainable
and makes updates a file edit rather than a prompt rewrite.

**Separate skills per domain.** A single "do everything" prompt produces mediocre results
across all domains. A tightly scoped skill with deep context on one domain produces
markedly better output than a generic prompt. Scope traded for quality.

## The Scoring Layer

The email skill got a measurement side: a single-file HTML scoring tool that checks
AI-drafted community emails against the organization's brand voice and terminology rules —
prohibited terms, required structural elements, tone in