# Issue #689 — Stellar SDK Migration

A focused workspace for a proposed contribution to [C-Address-Onboarding-Bridge issue #689](https://github.com/C-Address-Onboarding-Bridge/C-Address-Onboarding-Bridge--Contract/issues/689).

This repository is a planning and work log. It is not the upstream project and does not contain its source code.

## Objective

Move the upstream SDK and relayer from `@stellar/stellar-sdk` v12 to the current major, adapt the breaking APIs, restore a blocking high-severity npm audit, and verify the SDK and relayer.

## Drips status

Snapshot: 2026-09-27.

- Application submitted through Drips for Stellar Wave 9.
- The Drips profile screenshot showed 2 applications and 0 assigned issues. The upstream issue must be formally assigned before coding begins.
- Wave 9 is scheduled to end on 2026-09-30. Work must be resolved within the active Wave to earn points.
- The published Stellar Wave 9 pool is $75,000, shared by points; issue-level payment is variable and not guaranteed.
- Drips rewards are paid in USDC on Stellar and require identity verification before applying.

See [Drips contributor workflow](https://docs.drips.network/wave/contributors/solving-issues-and-earning-rewards/) and [Stellar Wave](https://www.drips.network/wave/stellar).

## Scope from upstream issue

- Upgrade `@stellar/stellar-sdk` to the current major.
- Migrate `SorobanRpc` to `rpc` and adapt any other changed APIs.
- Review SDK sources, deployment scripts, and the relayer.
- Add or update a Jest regression test.
- Make `npm audit --audit-level=high` blocking again.
- Pass SDK tests and relayer typecheck.
- Keep the pull request focused and link it with `Closes #689`.

## Initial technical findings

Verified against the upstream default branch on 2026-09-27:

- SDK package currently declares `@stellar/stellar-sdk: ^12.0.0`.
- Relayer package also declares `@stellar/stellar-sdk: ^12.0.0`.
- The root project engine currently permits Node.js `>=18.0.0`.
- CI's SDK audit job currently uses Node.js 20 and is marked `continue-on-error: true`.
- Direct old-namespace usage was found in `sdk/src/bridge.ts` and `sdk/src/events.ts`; the upstream issue also identifies `sdk/src/cachedBridge.ts`, `scripts/deploy.ts`, and the relayer.
- The Stellar JS SDK release page identified v17.1.0 as current on this date. Re-check the current stable release before implementation.

The current migration guide notes major-version changes beyond the RPC namespace, including a Node.js engine floor of 22.12.0 and changes to XDR and byte APIs. See the [official migration guide](https://stellar.github.io/js-stellar-sdk/guides/00-migration/) and [SDK releases](https://github.com/stellar/js-stellar-sdk/releases).

## Work rule

Do not begin upstream implementation until the maintainer assigns the issue through Drips. After assignment, re-check upstream HEAD, current SDK release, and the issue acceptance criteria before changing code.

## Documents

- [Technical plan](docs/TECHNICAL_PLAN.md)
- [Roadmap](docs/ROADMAP.md)
- [Checkpoint](docs/CHECKPOINT.md)

## License and attribution

All implementation work will be contributed to the upstream repository under its existing license. This planning repository contains no copied upstream source code.
