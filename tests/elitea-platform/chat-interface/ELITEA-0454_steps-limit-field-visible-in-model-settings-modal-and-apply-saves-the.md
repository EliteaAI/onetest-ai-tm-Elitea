---
id: ELITEA-0454
title: "Steps Limit Field Visible in Model Settings Modal and Apply Saves the Value"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3292]
---
# ELITEA-0454: Steps Limit Field Visible in Model Settings Modal and Apply Saves the Value

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the STEPS LIMIT field is present in the Model Settings modal in Chat, and that entering a new value and clicking Apply saves it correctly.

**Coverage:**
- STEPS LIMIT field appears in the modal alongside MAX COMPLETION TOKENS
- Field is a numeric input
- Field is accessible via the ⚙ icon next to the model selector
- Entering a new value and clicking Apply saves the value
- Reopening the modal shows the previously saved value
- Cancel button does not modify the saved value

## Preconditions

- Logged in to {{base_url}} with a valid user account
- Private project is selected
- At least one conversation exists or a new one is created
- Browser: Chrome (latest)

## Test Data

- Steps Limit initial value: default shown in modal (e.g. 25)
- Steps Limit new value: 5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat in the sidebar. Open any existing conversation or create a new one. | Chat conversation interface is displayed with model selector at the bottom. |
| 2 | Locate the model selector at the bottom of the chat input area (e.g. 'Anthropic Claude 4.6 Sonnet'). Click the ⚙ (gear/settings) icon to the right of the model selector label. | Model Settings modal opens. It contains MAX COMPLETION TOKENS section and STEPS LIMIT section with a numeric input field and an (ℹ) icon next to the label. |
| 3 | Note the current STEPS LIMIT value displayed. Clear the field and type '5'. | Field accepts the numeric value 5. |
| 4 | Click the Apply button. | Modal closes without error. |
| 5 | Open the Model Settings modal again. | STEPS LIMIT field shows '5' — the previously saved value. |
| 6 | Change the STEPS LIMIT field to '99' and click Cancel. | Modal closes. Saved STEPS LIMIT remains '5', not '99'. |

## Expected Final State

Modal closes. Saved STEPS LIMIT remains '5', not '99'.

## Pass/Fail Criteria

**Pass:**
- STEPS LIMIT field is present and labeled correctly in the modal
- Numeric input accepts a valid integer value
- Apply closes the modal and persists the entered value
- Reopening the modal shows the saved value
- Cancel does not overwrite the saved value

**Fail:**
- STEPS LIMIT field is absent from the modal
- Apply does not close the modal or shows an error for a valid integer
- Reopening shows the old value instead of 5
- Cancel unexpectedly overwrites the saved value
