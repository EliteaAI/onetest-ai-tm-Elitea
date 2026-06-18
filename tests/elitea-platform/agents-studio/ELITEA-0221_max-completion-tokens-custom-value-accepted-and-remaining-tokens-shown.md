---
id: ELITEA-0221
title: "Max Completion Tokens — Custom Value Accepted and Remaining Tokens Shown"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0221: Max Completion Tokens — Custom Value Accepted and Remaining Tokens Shown

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that entering a custom Max Tokens value is accepted and the Remaining Tokens field is displayed.

**Coverage:**
- Custom radio selectable with a user-defined Max Tokens value
- Remaining Tokens field appears and shows a value

## Preconditions

- Model Settings dialog is open for a published agent chat session

## Test Data

Max Tokens: 2048

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings dialog. | Dialog visible. |
| 2 | Select the Custom radio button. | Max Tokens input field becomes active. |
| 3 | Clear the Max Tokens field and enter 2048. | Field shows 2048. |
| 4 | Observe the Remaining Tokens field. | Remaining Tokens value is displayed. |
| 5 | Click Apply. | Dialog closes without error. |
| 6 | Reopen dialog. | Max Tokens shows 2048, Custom radio is selected. |

## Expected Final State

Max Tokens shows 2048, Custom radio is selected.

## Pass/Fail Criteria

**Pass:**
- Custom radio is selectable; Max Tokens input accepts 2048
- Remaining Tokens field shows a calculated value
- Value persists after Apply

**Fail:**
- Custom value is not accepted or causes validation error on valid input
- Remaining Tokens not shown when Custom is selected
