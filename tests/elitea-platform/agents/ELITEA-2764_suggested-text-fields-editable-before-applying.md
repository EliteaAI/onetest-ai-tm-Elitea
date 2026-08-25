---
id: ELITEA-2764
title: "Suggested text fields can be edited by the user before applying"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | General prompt requesting overall improvement |
| Manual edit appended | "v2" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI with a general prompt | Prompt accepted |
| 2 | Generate the draft and navigate to the General step | Suggested Name field is shown, editable |
| 3 | Modify the suggested Name by appending "v2" at the end | The field reflects the manual edit |
| 4 | Navigate to the next wizard step, then navigate back to General | General step reloads |
| 5 | Verify the manual edit ("v2") is still present in the Suggested Name field | Edit is retained across navigation |
| 6 | Complete the remaining wizard steps and apply changes | Modal closes without error |
| 7 | Verify the final Agent Name | Name includes the manually appended "v2" |

## Expected Final State

The Agent's Name reflects the user's manual edit to the AI suggestion, not just the raw AI-generated text.

## Pass/Fail Criteria

**Pass:**
- The manual edit is retained through step navigation and present in the final applied value

**Fail:**
- The manual edit is lost on navigation or reverted to the original AI suggestion after applying
