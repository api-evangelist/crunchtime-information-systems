# Crunchtime Information Systems

Crunchtime (Crunchtime Information Systems) is a Boston-based provider of AI-powered operations-management software for multi-unit restaurants — founded in 1995, serving 850+ restaurant brands across 150,000+ locations. The platform unifies inventory management, labor scheduling, kitchen/operations execution, and analytics.

Crunchtime publishes a public developer hub (https://developer.crunchtime.com/) for its Inventory & Labor and Cruise data-integration REST APIs — custom header-based token auth, page-based pagination, documented rate limits (500 calls / 5s), and incremental sync via `minutesSinceUpdate`.

Backed by: Battery Ventures

## Enrichment artifacts
- `authentication/` — custom header token auth (authenticationtoken + sitename + userid + password)
- `conventions/` — List/Page/Save access patterns, pagination, incremental sync, timeouts
- `rate-limits/` — 500 req / 5s, batch/list/page limits
- `changelog/` — recent dated developer-hub releases
- `sandbox/` — test vs production token/host separation
- `mcp/` — candidate MCP tool surface derived from documented operations
- `skills/` — packaged Agent Skills grounded in real operationIds
- `security/` — domain-security probe + trust center (SOC 2, ISO 27001 via trust.crunchtime.com)
- `llms/` — developer-hub llms.txt (verbatim)
