---
status: blocked
canonical: false
priority: 1
area: security
created: 2026-11-03
last_updated: 2026-11-03
---

# SPEC-022 Security hardening continuation

## User-Visible Behavior

- Vendor members without the required permission cannot invite administrator members.
- Vendor-facing seller retrieval does not expose payment or professional details that are restricted to authorized contexts.
- Vendor uploads accept only supported media types and do not advertise SVG uploads in the Vendor UI.
- Cart validation prevents a seller from adding or shipping another seller's offer through a crafted request.
- Payout calculations include every applicable refund credit line, including lines with a reason.
- Admin store forms expose only reachable lifecycle transitions and enforce status, premium, and cache rules through permissions.
- Payout widgets and account detail screens request the payout data they display.

## Verification

1. Install with `bun install --frozen-lockfile`.
2. Run `bun run lint` and `bun run build`.
3. Run focused seller member, seller route, cart, upload, payout amount, and admin store lifecycle tests.
4. Review the changed files for authorization, field restriction, input filtering, and cache invalidation regressions.
5. Record command output and pass/fail evidence below.

## Evidence

- 2026-11-03: Inherited upstream commit `953b89465` records the security review fixes; focused verification in this continuation is pending.
- 2026-11-03: Continuation branch created as `fix/core-security-hardening-follow-up`; no new functional code changes yet.
- 2026-11-03: `bun install --frozen-lockfile` installed 2216 packages successfully.
- 2026-11-03: `bun run lint` completed with 0 errors and 2192 warnings.
- 2026-11-03: `bun run build` completed successfully with 13/13 tasks passing in 1m43s.
- 2026-11-03: Focused unit verification passed: 5 suites and 51 tests covering route permissions, permission middleware, cart credit allocation, payout validators, and payout amounts.
- 2026-11-03: Focused HTTP verification is blocked by missing PostgreSQL service. Six selected suites reached bootstrap but failed while creating temporary databases with `AggregateError`; no application assertions were counted as passing. Redis used the test fake because no Redis service is installed.

## Notes

The source fork did not contain tracked `docs/specs/` files because its `.gitignore` excluded that directory. This file is now tracked so the active workstream and evidence remain available to the next contributor. The spec remains `blocked` until PostgreSQL-backed HTTP verification runs; the build and focused unit checks are green.
