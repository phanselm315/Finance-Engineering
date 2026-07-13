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
prohibited terms, required structural elements, tone indicators — with per-rule pass/fail
and an overall grade. Two decisions carried it: **HTML over a Python script**, because
the person reviewing emails is not running Python scripts, and **rule-based scoring over
AI scoring**, because the rules are explicit and enumerable — hard-coded checks are
faster, more transparent, and easier to audit. Building the rubric before scaling email
volume surfaced several places where the style guidelines themselves were ambiguous or
contradictory, and those got resolved before they became recurring problems.

## Case Study: the Resume Skill

Built after enough manual tailoring sessions to recognize the pattern was worth
formalizing. Provide a job description; it produces a tailored version of a formatted
master resume, selecting from a bank of pre-approved language rather than generating
from scratch — resumes require specific, defensible language, not creative writing. Each
real use refined the language bank and edge-case handling; the skill got noticeably
better after each one, because each one fed an update. The general lesson: formalize a
workflow into a skill *after* you've done it manually enough times to know where the
friction and the judgment calls actually are.

## Lessons Learned

A well-structured system prompt with hard rules and rich context is 10x more useful than
a generic prompt.

The investment in building these skills upfront compounds across every session. Work that
used to take an hour of back-and-forth now takes five minutes because the context is
already loaded.

---

*Part of [Finance Engineering](../../README.md)*
