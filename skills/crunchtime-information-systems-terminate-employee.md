---
name: Terminate an employee
description: Mark an existing Crunchtime employee as terminated and confirm the change.
api: https://developer.crunchtime.com/
operations: [getEmployeeV1, saveEmployeeV1]
generated: '2026-07-18'
method: generated
---

# Terminate an employee

Mirror of the developer-hub "Terminate an Employee" recipe.

## Authentication
Send `authenticationtoken`, `sitename`, `userid`, `password` on every request.

## Steps
1. **Load the current record.** Call `getEmployeeV1` with the employee number and site to retrieve the existing employee payload.
2. **Set termination.** Call `saveEmployeeV1` (POST) with the same identifiers and the termination fields (status/termination date) set per the Employee schema. Save operations create-or-update, so re-posting the existing record with termination data updates it in place.
3. **Verify.** Call `getEmployeeV1` again to confirm the terminated status persisted.

## Rules
- Stay under 500 calls / 5 seconds (429 on breach).
- Load-then-save to avoid clobbering fields; there is no idempotency-key contract.
