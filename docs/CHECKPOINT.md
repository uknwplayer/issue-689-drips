# Checkpoint — 2026-09-27

## Objective

Prepare a focused contribution to [upstream issue #689](https://github.com/C-Address-Onboarding-Bridge/C-Address-Onboarding-Bridge--Contract/issues/689): upgrade the Stellar JS SDK from v12 to the current major, adapt breaking APIs, restore a blocking high-severity npm audit, and verify the SDK and relayer.

## Current state

- Dedicated public repository: [uknwplayer/issue-689-drips](https://github.com/uknwplayer/issue-689-drips)
- Planning documents added; no upstream code has been copied or changed.
- Drips application submitted on 2026-09-27.
- Latest screenshot showed 2 applications, 0 assigned issues, 0 points, and 0 resolved issues.
- Do not start implementation until the maintainer assigns issue #689 through Drips.
- Stellar Wave 9 was listed to end 2026-09-30. Reconfirm the deadline before starting.

## Evidence and facts checked

- Upstream SDK and relayer both depend on `@stellar/stellar-sdk ^12.0.0`.
- Root package engine allows Node.js `>=18.0.0`.
- CI's SDK audit job uses Node.js 20 and has `continue-on-error: true`.
- Official Stellar JS SDK release page listed v17.1.0 on 2026-09-27.
- Official migration materials identify Node.js `>=22.12.0` and additional XDR/byte API changes in the current major.
- One other application comment was present on the upstream issue at the last GitHub check; no open PR was found. Re-check both before coding.

## Next action

Wait for assignment. If assigned, revalidate upstream HEAD, current SDK release, issue status, and Wave deadline, then update this checkpoint before implementation.
