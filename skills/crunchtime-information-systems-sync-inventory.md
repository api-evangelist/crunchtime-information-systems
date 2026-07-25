---
name: Sync physical inventory counts
description: Push physical inventory counts into Crunchtime and read back current inventory levels.
api: https://developer.crunchtime.com/
operations: [getAllLocationsV1, savePhysicalInventoryStandards, getCurrentInventoryByPage]
generated: '2026-07-18'
method: generated
---

# Sync physical inventory counts

Submit a location's physical count and confirm resulting inventory levels.

## Authentication
Send `authenticationtoken`, `sitename`, `userid`, `password` on every request.

## Steps
1. **Resolve the location.** Call `getAllLocationsV1` (or `getLocationsByPageV1`) to get the site for the count.
2. **Submit counts.** Call `savePhysicalInventoryStandards` (POST) with the counted products and quantities for that location. Batch up to 50 records per call; split larger counts across calls.
3. **Read back.** Call `getCurrentInventoryByPage` for the location to verify current inventory levels after the count posts. Use the `...ByPage` paging (default 10/page) for large product sets.

## Rules
- Rate limit 500 / 5s; List operations cap at 500,000 records, so prefer paged reads.
- No idempotency key — de-duplicate before re-submitting counts.
