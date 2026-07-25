---
name: Onboard a new employee
description: Create a new employee record in Crunchtime for the correct location and verify it saved.
api: https://developer.crunchtime.com/
operations: [getAllLocationsV1, saveEmployeeV1, getEmployeeV1]
generated: '2026-07-18'
method: generated
---

# Onboard a new employee

Use the Crunchtime Inventory & Labor API to create an employee at the right location.

## Authentication
Send all four headers on every request: `authenticationtoken`, `sitename`, `userid`, `password`. Use a dedicated Application User's token (test token + test sitename against `https://webservices-test.net-chef.com` while developing; production token + production sitename against `https://webservices.net-chef.com`).

## Steps
1. **Find the location.** Call `getAllLocationsV1` and select the target location/site the employee belongs to. (For large chains use `getLocationsByPageV1` to page through.)
2. **Create the employee.** Call `saveEmployeeV1` (POST) with the employee number, the resolved site, and the employee's details. You may submit up to 50 records in one Save call.
3. **Verify.** Call `getEmployeeV1` with the new employee number and site to confirm the record persisted.

## Rules
- Rate limit: 500 calls per 5 seconds — a 429 means back off.
- No idempotency key is supported; make `saveEmployeeV1` conditional by first checking existence with `getEmployeeV1`/`getEmployeeNumbersV1` to avoid duplicates.
- Errors surface as HTTP status codes (400 validation, 401/403 auth, 429 rate limit).
