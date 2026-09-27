# Roadmap

## Phase 0 — Eligibility and assignment

- [x] Create a dedicated planning repository.
- [x] Submit a Drips application for upstream issue #689.
- [ ] Confirm the maintainer assigns the issue in Drips.
- [ ] Re-check the current Wave deadline and issue status.

**Gate:** No upstream coding before assignment.

## Phase 1 — Fresh baseline

- [ ] Record upstream HEAD SHA and inspect changes since initial review.
- [ ] Confirm current stable SDK version and migration guidance.
- [ ] Inventory all SDK imports and version-sensitive APIs.
- [ ] Run baseline SDK and relayer checks.

## Phase 2 — Migration

- [ ] Upgrade SDK and relayer dependencies and regenerate the lockfile.
- [ ] Align Node.js engine constraints, CI, and docs.
- [ ] Migrate RPC, XDR, byte, and any other changed APIs.
- [ ] Add focused regression coverage.

## Phase 3 — Audit and validation

- [ ] Make high-severity SDK audit blocking after it passes.
- [ ] Pass SDK typecheck, build, tests, and lint.
- [ ] Pass relayer typecheck.
- [ ] Review changes for scope, compatibility, and accidental lockfile churn.

## Phase 4 — Upstream contribution

- [ ] Open PR with `Closes #689`.
- [ ] Respond to maintainer feedback and rerun affected checks.
- [ ] Confirm PR merge and issue resolution in Drips during the active Wave.
- [ ] Confirm points/reward grant appears in Drips.

## Current state

As of 2026-09-27, the application is submitted but the screenshot showed 0 assigned issues. The active Wave was listed to end on 2026-09-30. Rewards are proportional to points and are not a fixed issue price.
