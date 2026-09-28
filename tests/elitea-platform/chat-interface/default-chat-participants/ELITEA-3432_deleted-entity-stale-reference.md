---
id: ELITEA-3432
title: "Deleting an Agent or Pipeline Does Not Remove It From Default Chat Configuration (Known Gap)"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, story:6358, default-chat-config, known-gap, edge-case]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3432: Deleting an Agent or Pipeline Does Not Remove It From Default Chat Configuration (Known Gap)

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the currently-known gap: deleting an agent or pipeline that is a preconfigured chat participant does **not** automatically remove it from "Default Chat Configuration" and produces no warning at delete time — and confirm the stale entry can be manually cleaned up from Settings.

**Coverage:** Confirmed gap, flagged for follow-up — this case documents current behavior explicitly rather than assuming auto-cleanup exists.

## Preconditions

- Admin access to Project Settings → "Default Chat Configuration"
- An agent or pipeline not needed for other tests, safe to delete

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Add an agent (or pipeline) as a preconfigured participant and Save. | Participant is saved. |
| 2 | Delete that agent/pipeline from the project entirely. | Deletion completes — **no warning is shown** that it's referenced as a preconfigured chat participant (current known behavior). |
| 3 | Return to Project Settings → "Default Chat Configuration". | The now-deleted entity is **still listed** (stale reference) — confirms the known gap. |
| 4 | Open a new chat. | Record actual behavior: is the stale participant silently skipped, does it show an error, or does the panel break? |
| 5 | In Settings, manually remove the stale entry from the list (via its "×") and Save. | The stale entry is successfully removed and does not reappear on reload. |

## Expected Final State

Current behavior: no auto-removal and no delete-time warning (confirmed gap, worth raising as a future enhancement); manual removal via Settings works correctly as the workaround.

## Pass/Fail Criteria

**Pass:**
- Step 5 (manual removal) succeeds and persists — this is the one thing that must work today
- Step 4's actual behavior is recorded, whatever it is

**Fail:**
- Manual removal in step 5 doesn't stick, or step 4 causes a crash/broken panel rather than a graceful skip or clear error

**Note:** Steps 2–3 are *expected* to show the gap per current implementation — this is not itself a failing result, but should be raised with the dev team as a suggested improvement (auto-remove-on-delete, or a delete-time warning).
