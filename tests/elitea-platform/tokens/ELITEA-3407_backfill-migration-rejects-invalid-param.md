---
id: ELITEA-3407
title: "Backfill Migration Task Rejects Unrecognized param Values"
priority: low
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, migration]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3407: Backfill Migration Rejects Unrecognized `param`

**Module:** Tokens · **Priority:** Low · **Type:** Negative

**Objective:** Confirm the `migrate_user_system_tokens` admin task validates its `param` input strictly — only `"dry_run"` (any case/whitespace variant) or no param at all are accepted; anything else raises a clear, actionable error instead of silently misinterpreting intent (e.g. accidentally running for real when a typo'd dry-run flag was intended).

**Coverage:** Design detail from `admin`#45 — `is_dry_run()` validation, explicit `ValueError` on unrecognized input

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run `migrate_user_system_tokens` with `param="dryrun"` (no underscore — a plausible typo). | Task raises `ValueError: Unrecognized param 'dryrun': pass 'dry_run' to rehearse, or nothing at all to write`. No tokens are written. |
| 2 | Run with `param="true"`. | Same rejection pattern — raises `ValueError` naming the actual unrecognized value, no writes occur. |
| 3 | Run with `param=""` (empty string). | Treated as "no param" — proceeds as a real run (per `is_dry_run()`'s documented `""`/`None` → False behavior), not rejected. |
| 4 | Run with no `param` key at all. | Same as step 3 — real run, not rejected. |

## Expected Final State

Only a genuinely empty/absent param or a recognizable dry-run token is accepted; any other string is rejected before any DB write is attempted.

## Pass/Fail Criteria

**Pass:**
- Unrecognized param values raise the documented `ValueError` with no side effects; empty string and absent param both correctly proceed as real runs

**Fail:**
- An unrecognized param is silently accepted (either treated as dry-run or as a real run) instead of raising
- The error message doesn't name the offending value, making the mistake hard to diagnose
