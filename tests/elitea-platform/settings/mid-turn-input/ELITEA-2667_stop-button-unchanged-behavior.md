---
id: ELITEA-2667
title: "Verify Stop button behavior unchanged when Mid-turn Input enabled"
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start an agent turn (without sending mid-turn input) | Agent begins generating |
| 2 | Verify Stop button appears | Stop button is visible |
| 3 | Click Stop button | Agent stops generating |
| 4 | Verify partial response preserved | Partial content is visible |
| 5 | Verify conversation can continue | New messages can be sent |

## Expected Final State

Stop button works exactly as before when mid-turn input feature is enabled but not used.

## Pass/Fail Criteria

**Pass:**
- Stop button appears and functions normally
- Behavior identical to pre-feature implementation

**Fail:**
- Stop behavior differs from expected
- New bugs introduced
