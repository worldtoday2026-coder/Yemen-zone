# Yemen-zone Continuation Plan

## Baseline and source of truth

This continuation starts from `fix/core-security-hardening-follow-up`, based on the latest verified security-hardening work available on the Mercur upstream remote. The fork's `main` branch was last updated on 2026-10-26, while the upstream security branch contains the 2026-11-03 review fixes and the merged product-index work.

The repository is a Mercur.js marketplace platform with a Medusa core, Admin and Vendor panels, Store API, payout integrations, and a typed dashboard extension system. The implementation must preserve the existing Bun/Turborepo workflow and the security boundaries documented in `docs/PRODUCT.md` and `docs/ARCHITECTURE.md`.

## Current workstream

The active workstream is security-hardening verification and follow-up. The inherited changes cover seller member permissions, restricted seller fields, upload filtering, cart seller validation, payout refund arithmetic, and administrative store lifecycle permissions. Before adding new product behavior, the branch must be installed and verified so any regression is isolated from the inherited changes.

## Execution order

1. Install dependencies with the repository's required Bun toolchain and verify the lockfile.
2. Run the repository lint and build checks; record exact results and any environmental blockers.
3. Run focused integration and unit suites covering seller members, seller routes, cart validation, uploads, payout amounts, and admin store lifecycle behavior.
4. Inspect failures against the inherited commits. Fix only failures within the security-hardening scope, adding or extending regression tests for every behavioral fix.
5. Keep the work restartable from `bun install && bun run dev` and update this plan, the task log, and the progress handoff after each meaningful checkpoint.
6. Push the branch to `Yemen-zone` and commit only safe, reviewable units. Do not merge into `main` without explicit approval.

## Repository structure relevant to this work

- `packages/core/src/api` and `packages/core/src/workflows`: backend permissions, validation, uploads, cart, seller, and payout behavior.
- `integration-tests/http`: endpoint-level regression coverage.
- `packages/admin` and `packages/vendor`: dashboard permission gates, forms, and payout/upload UI.
- `apps/api`: starter runtime and operational scripts.
- `docs`: durable project, architecture, and continuation records.

## Constraints and decisions

- Use Bun only; do not substitute npm, Yarn, or pnpm.
- Do not expose secrets in source, logs, or committed documentation.
- Keep one active security workstream at a time.
- Preserve existing APIs unless a security correction requires a contract change; document such changes in the task log.
- Every completed task must include evidence before it is marked complete.
