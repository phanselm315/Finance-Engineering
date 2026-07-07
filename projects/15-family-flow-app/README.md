# Family Flow App

**Status:** 🔄 Active  
**Started:** Mar 2026 (bulk: May 2026)  

## What This Is

Personal household app combining shared calendar aggregation, unofficial API integration
with a grocery store, a financial dashboard, Plaid integration, and a
Supabase-backed cash flow predictor. Built for real daily use by my family.

## Architecture

- **Backend:** Supabase (PostgreSQL + auth + realtime)
- **Calendar:** Aggregation layer pulling from multiple family calendars into a single
  shared view
- **Grocery integration:** Unofficial API wrappers for a major grocery chain — weekly
  deals and inventory pulled automatically (see Key Decisions)
- **Financial dashboard:** Household spending tracking and categorization
- **Plaid integration:** Connecting spouse's accounts for unified financial view
  (in progress)
- **Cash flow predictor:** Model logic built on Supabase — forecasting household cash
  position (in progress)

## Key Decisions

**Use the app's own API rather than build a scraper.** The grocery chain has
no public API. The options were: scrape the website (brittle, slow, breaks on layout
changes) or figure out what the app is calling. Claude Code worked out the integration
from the app's network behavior.
The result is a proper API wrapper that calls the same endpoints the app uses — faster
and more reliable than scraping.

**Supabase over a simpler backend.** The cash flow predictor needs persistent state,
realtime updates, and will eventually share data across multiple users (family members).
Supabase handles all of it without requiring a custom backend. The complexity is
justified by the feature requirements.

**Build for the actual users, not for the demo.** The primary end user for most of these
features is my wife. Every UI and workflow decision gets validated against whether she'll
use it, not whether it's technically elegant.

## Lessons Learned

The grocery API work was the hardest piece in this project. It took iteration until the
wrappers held reliably. This is a different level of engineering than calling a
documented API — it
requires patience, systematic testing, and comfort with incomplete information.

Building for family use is the most demanding form of user testing. There's no polite
feedback. If something is confusing or broken, you hear about it immediately.

---

*Part of [Finance Engineering](../../README.md)*
