---
id: ELITEA-2662
title: "Verify Regenerate functionality on response that used mid-turn input"
priority: high
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
- User has completed a turn with mid-turn interaction

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Complete a turn with mid-turn input | Turn completes with mid-turn message incorporated |
| 2 | Locate the Regenerate button on the agent's response | Regenerate button is visible |
| 3 | Click Regenerate | Agent regenerates the response |
| 4 | Wait for regeneration to complete | New response is generated |
| 5 | Verify the new response | Regenerated response still considers mid-turn context |

## Expected Final State

Regenerate works correctly on responses that incorporated mid-turn input, maintaining proper context.

## Pass/Fail Criteria

**Pass:**
- Regenerate button works
- New response is generated
- Mid-turn context is maintained in regeneration

**Fail:**
- Regenerate fails or errors
- Mid-turn context is lost in regeneration
