---
id: ELITEA-2668
title: "Verify Human-in-the-loop approval flow unaffected by Mid-turn Input feature"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- Agent or pipeline configured with human-in-the-loop approval step

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Agent/Pipeline | One with HITL configured |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a flow that requires HITL approval | Flow starts, reaches approval step |
| 2 | Verify approval UI appears | Approval dialog/interface shown |
| 3 | Approve or reject the action | Action processed based on decision |
| 4 | Verify flow continues/stops appropriately | Behavior matches approval decision |

## Expected Final State

Human-in-the-loop approval flows work exactly as before, unaffected by mid-turn input feature.

## Pass/Fail Criteria

**Pass:**
- HITL approval UI appears correctly
- Approval/rejection processed normally

**Fail:**
- HITL flow broken or changed
- Approval interface missing
