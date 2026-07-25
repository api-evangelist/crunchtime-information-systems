---
name: Incrementally pull changed records
description: Use minutesSinceUpdate to fetch only recently changed Crunchtime records instead of full extracts.
api: https://developer.crunchtime.com/
operations: [getCompanyProductsEnhancedByPage, getRecipesEnhancedByPageV2]
generated: '2026-07-18'
method: generated
---

# Incrementally pull changed records

Mirror of the developer-hub "How to Retrieve Recently Updated Records using minutesSinceUpdate" recipe. Avoid re-pulling entire data sets each run.

## Authentication
Send `authenticationtoken`, `sitename`, `userid`, `password` on every request.

## Steps
1. **Pick a window.** Compute the minutes since your last successful sync. The `minutesSinceUpdate` cap is 1 month (enforced on the Company Product Enhanced service as of 2026-07-14) — for longer gaps, fall back to a full paged extract.
2. **Page through changes.** Call `getCompanyProductsEnhancedByPage` (or `getRecipesEnhancedByPageV2`, or any `...ByPage` GET) with `minutesSinceUpdate` set to your window; iterate pages (default 10 records/page) until exhausted.
3. **Persist a checkpoint.** Record the sync timestamp so the next run's `minutesSinceUpdate` covers only new changes.

## Rules
- Rate limit 500 calls / 5 seconds; use a low-parallelism, sequential paging pattern for stability.
- List (getAll...) operations return up to 500,000 records — prefer paged + minutesSinceUpdate for incremental jobs.
