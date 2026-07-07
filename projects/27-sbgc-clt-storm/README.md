# SBGC CLT — STORM / Co-STORM Research Synthesis

**Status:** ⏸️ Paused — first run underdelivered; rebuild planned  
**Started:** June 2026  

## What This Is

A test of Stanford's **STORM** and **Co-STORM** — open-source systems that generate
grounded, Wikipedia-style articles by simulating a multi-perspective conversation among AI
agents and writing only from retrieved sources (Co-STORM adds a human to that roundtable).
I ran it for two reasons at once: to learn the STORM/Co-STORM workflow hands-on, and to use
it as a way to review the community land trust (CLT) research a community group I work with
(SBGC) has already accumulated — to see whether the method could pressure-test and extend
our own thinking.

## Architecture

- **Corpus build** — assembled a source corpus on community land trusts to ground the
  generation, rather than letting the system retrieve open-web only.
- **STORM pass** — the multi-agent outline-and-draft pipeline: simulated expert
  perspectives ask questions, retrieve against the corpus, and synthesize a structured
  article with citations.
- **Co-STORM pass** — the collaborative-discourse variant, with me joining the agent
  roundtable to steer the inquiry instead of running it fully hands-off.

## Key Decisions

**Run it on real, owned material, not a toy topic.** Pointing the method at our actual CLT
research was the whole point — a method test that also moves a real project forward, or
exposes why it doesn't.

**Two variants, same topic.** Running both STORM and Co-STORM on the same material is the
cleanest way to feel the difference between hands-off generation and human-in-the-loop
steering.

## Lessons Learned

The results were weak, and the cause was instructive: **anchoring on a single referenced
document narrowed and biased the output.** Leaning on one source pulled the synthesis toward
that document's framing and crowded out the broader corpus the method is built to range
across — the opposite of what STORM's multi-perspective design is for. The honest read is
that I constrained the tool into producing a paraphrase rather than a synthesis.

Logged as a negative-but-useful result, in the same spirit as the Kalshi write-up: the run
underdelivered, and knowing *why* is the deliverable. The rebuild is to feed a broader,
better-balanced corpus and stop hand-feeding a single anchor doc, then re-run both passes
and compare.

---

*Part of [Finance Engineering](../../README.md)*
