# Technical Plan — SDK Major Migration

## Status

Planning only. The contributor application has been submitted, but the issue was not yet assigned in the latest user-provided Drips screenshot. Per the Drips workflow, implementation starts after assignment.

## Upstream baseline inspected

Repository: [C-Address-Onboarding-Bridge/C-Address-Onboarding-Bridge--Contract](https://github.com/C-Address-Onboarding-Bridge/C-Address-Onboarding-Bridge--Contract)

- `sdk/package.json`: `@stellar/stellar-sdk ^12.0.0`
- `relayer/package.json`: `@stellar/stellar-sdk ^12.0.0`
- Root `package.json`: Node.js `>=18.0.0`
- `.github/workflows/ci.yml`: SDK audit uses Node.js 20 and currently continues on error.
- Old `SorobanRpc` namespace appears in the SDK bridge and event subscriber. The bounty issue also calls out `cachedBridge.ts`, deployment scripts, and the relayer.

Revalidate all of the above against upstream HEAD after assignment. This plan is not a substitute for that check.

## Migration constraints found in official sources

As of 2026-09-27, the official release page lists `@stellar/stellar-sdk 17.1.0` as the current release. Confirm the latest stable release at implementation time.

The official migration guide and release notes identify relevant major changes:

- Node.js requirement: `>=22.12.0`.
- XDR namespace/API modernization in v17.
- Public byte-returning APIs use `Uint8Array` where earlier versions exposed Node `Buffer`.
- The RPC namespace is `rpc`; check other imports and method signatures from v12 instead of doing a text-only rename.

Sources:

- [SDK migration guide](https://stellar.github.io/js-stellar-sdk/guides/00-migration/)
- [SDK releases](https://github.com/stellar/js-stellar-sdk/releases)

## Implementation sequence (after assignment)

1. **Revalidate and inventory**
   - Record upstream HEAD SHA and current bounty assignment.
   - Confirm current stable SDK version, migration guide, Node requirements, and security advisories.
   - Search all SDK, relayer, scripts, tests, examples, and CI for SDK imports, RPC types, XDR calls, Buffer assumptions, and deep imports.
   - Capture baseline test, typecheck, and audit results.

2. **Upgrade dependency and runtime**
   - Update the SDK workspace and relayer dependency declarations.
   - Update the lockfile using the repository's workspace installation procedure.
   - Align root/package engine constraints, CI Node setup, and contributor documentation with the SDK requirement.
   - Avoid unrelated dependency upgrades.

3. **Adapt APIs**
   - Replace old Soroban RPC namespace/types with the supported current API.
   - Resolve TypeScript errors from XDR and byte API changes.
   - Update deployment and relayer code wherever it consumes changed SDK symbols.
   - Preserve serialized values and transaction behavior; add conversion helpers only where required.

4. **Add regression coverage**
   - Add a focused Jest test that exercises at least one migration-sensitive boundary (RPC client construction or byte/XDR conversion) and would fail against the old implementation.
   - Extend existing tests for each changed public behavior; avoid tests that only duplicate a symbol rename.

5. **Restore blocking audit**
   - Run `npm audit --audit-level=high` in the SDK workspace after the upgrade.
   - Resolve high-severity findings within scope.
   - Remove `continue-on-error` from the SDK audit step only after the command passes on the supported Node version.
   - Do not silence findings with broad audit exceptions.

6. **Verify and submit**
   - Run SDK typecheck, build, Jest tests, and lint.
   - Run relayer typecheck.
   - Run the blocking SDK audit and relevant CI jobs.
   - Review the final diff for unrelated changes and document migration/runtime requirements.
   - Open an upstream PR including `Closes #689`; monitor CI and maintainer review.

## Verification checklist

- [ ] Revalidated upstream HEAD and issue assignment
- [ ] Confirmed current stable SDK release and official migration notes
- [ ] SDK dependency, relayer dependency, and lockfile are consistent
- [ ] Runtime engine and CI Node versions meet the current SDK requirement
- [ ] No unsupported old `SorobanRpc` imports/types remain
- [ ] XDR and Buffer/Uint8Array boundaries are reviewed and tested
- [ ] Focused regression test added
- [ ] SDK typecheck, build, tests, lint pass
- [ ] Relayer typecheck passes
- [ ] `npm audit --audit-level=high` passes
- [ ] Audit is blocking in CI
- [ ] PR is focused and links issue #689
