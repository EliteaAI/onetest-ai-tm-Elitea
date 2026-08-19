---
id: ELITEA-2650
title: "Mid-turn Input (Beta) Toggle in Chat Section"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:chat, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---
# ELITEA-2650: Mid-turn Input (Beta) Toggle in Chat Section

**Module:** Default Modules · **Priority:** High · **Type:** Functional

**Objective:** Verify the Mid-turn Input (Beta) toggle in the Chat section of Settings → General works correctly and its state persists.

**Coverage:**
- Mid-turn Input toggle is visible in Chat section
- Toggle can be enabled and disabled
- Toggle state persists after page refresh
- Feature description is accurate

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Feature description: "Send a message to an agent while it is still working, to steer the rest of the run."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General. | Settings page loads. |
| 2 | Scroll down to locate the "Chat" section below Default Modules. | Chat section is visible. |
| 3 | Verify "Mid-turn Input (Beta)" toggle is present. | Toggle is visible with label "Mid-turn Input (Beta)". |
| 4 | Verify the description text is displayed. | Description reads: "Send a message to an agent while it is still working, to steer the rest of the run." |
| 5 | Check the initial state of the toggle. | Toggle is  OFF. |
| 6 | Click the toggle to change its state. | Toggle switches to the opposite state. |
| 7 | Refresh the page. | Page reloads. |
| 8 | Navigate to Settings → General → Chat section. | Chat section displayed. |
| 9 | Verify the toggle state persisted. | Toggle is in the state set in step 6. |
| 10 | Toggle it back to the original state. | Toggle switches back. |
| 11 | Refresh and verify persistence again. | Original state restored and persisted. |

## Expected Final State

Mid-turn Input (Beta) toggle functions correctly with state persistence.

## Pass/Fail Criteria

**Pass:**
- Mid-turn Input toggle is visible in Chat section
- Toggle can be switched ON and OFF
- Description text is accurate and visible
- Toggle state persists after page refresh

**Fail:**
- Toggle is missing from Chat section
- Toggle cannot be changed
- Description is missing or incorrect
- Toggle state does not persist
