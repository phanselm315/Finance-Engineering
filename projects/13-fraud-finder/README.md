# Public-Records Relationship Mapper (Fraud Finder)

**Status:** ⏸️ Paused  
**Started:** May 2, 2026  

## What This Is

Public-data scraper and relationship-mapping pipeline. Pulls Illinois state contract data,
entity registrations, and political contribution records, then uses Claude to flag
connections between newly formed LLCs, contractors, and politicians that merit a human
look. First multi-stage data pipeline in the portfolio — Claude at exactly one step,
the scoring.

## Architecture

- **Runtime:** Python
- **Data sources (all public record):**
  - Illinois state contract awards database
  - Illinois Secretary of State entity registrations
  - Illinois political contribution records
- **Pipeline:**
  1. Scrape — pull and normalize records across sources
  2. Parse — extract entity names, dates, dollar amounts, principals
  3. Correlate — link entities across datasets (name matching, address overlap, formation dates)
  4. Flag — Claude evaluates connection patterns and scores which merit review
- **Output:** Flagged relationship maps with supporting data citations

**Pattern:** Search → parse → correlate → flag. Each stage feeds the next.
Claude handles the one judgment step (what's worth a look vs. coincidental); code
handles data extraction and normalization.

## Key Decisions

**Public data only.** Everything this pipeline touches is available to any citizen. No
credentials, no scraping behind logins, no gray areas. The point is to demonstrate what
can be found in data that's already public and already paid for by taxpayers.

**Claude for the reasoning step, code for the data layer.** The pattern-matching and
correlation work is deterministic enough for code. The judgment call — "is this actually
worth review or just a common name?" — requires reasoning. That's the one place Claude
earns its spot in the pipeline.

**Flag, don't conclude.** The output is flagged connections with supporting data, not
accusations. The system surfaces what's worth a human look; it doesn't make the call.
That's the right design for any investigative tool.

## Lessons Learned

This was the point where "using AI" became "designing a pipeline." The difference: an AI
tool answers a question. A pipeline executes a multi-step process, passing outputs forward
as inputs, and handles failures at each stage independently.

Public data is dramatically underused for accountability work. The data exists; the
barrier has always been the time required to cross-reference it.

---

*Part of [Finance Engineering](../../README.md)*
