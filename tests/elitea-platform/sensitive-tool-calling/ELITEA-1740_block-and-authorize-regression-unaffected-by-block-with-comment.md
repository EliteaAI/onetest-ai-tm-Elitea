---
id: ELITEA-1740
title: "Block and Authorize Actions Regression — Unaffected by Block with Comment Addition"
priority: critical
type: regression
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1740: Block and Authorize Actions Regression — Unaffected by Block with Comment Addition

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the existing Authorize and Block actions continue to work exactly as before — the addition of Block with Comment must not change their behavior.

## Preconditions

- At least one sensitive tool configured (e.g., `github.create_pull_request`)
- Agent chat is open with authorization dialog displayed

## Test Data

| Field | Value |
|-------|-------|
| Tool | `github.create_pull_request` |

## Steps — Part A: Authorize still works

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger the sensitive tool dialog | Dialog shown with all three buttons |
| 2 | Click **Authorize** | Dialog closes immediately |
| 3 | Observe agent response | Agent completes execution; tool side effect occurs (PR created) |
| 4 | Verify no comment-related payload attached | Agent output shows no spurious `user_feedback` field or comment reference |

## Steps — Part B: Block still works

| # | Action | Expected Result |
|---|--------|----------------|
| 5 | Trigger the sensitive tool dialog again in a new turn | Dialog shown |
| 6 | Click **Block** | Dialog closes immediately without expanding a text area |
| 7 | Observe agent response | Agent produces blocked-action acknowledgement (generic, no comment) |
| 8 | Verify the tool did NOT execute | No side effect (no PR created) |

## Expected Final State

Authorize and Block behave identically to their pre-#5318 behavior. No unintended comment injection on Authorize. No text area shown on Block.

## Pass/Fail Criteria

**Pass:**
- Authorize executes tool; Block prevents it
- Clicking Block goes directly to blocked state without showing text area
- Authorize does not attach `user_feedback` to the LLM response
- Both actions complete without errors

**Fail:**
- Block now shows text area unexpectedly
- Authorize attaches spurious comment to LLM context
- Either action broken or producing errors after #5318 changes
