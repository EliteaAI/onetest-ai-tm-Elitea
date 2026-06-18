---
id: ELITEA-0204
title: "TC-002: \"Publish Version\" Modal Opens With All Required UI Elements"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0204: TC-002: "Publish Version" Modal Opens With All Required UI Elements

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the "Publish" button opens the "Publish version" modal with the correct 3-step stepper, all required fields, and that closing the modal without completing the flow does not trigger any publish action.

Coverage:
- Modal title reads "Publish version"
- 3-step stepper shown: Preparation → Validation → Publishing (Preparation active on open)
- Instruction text: "Enter a version name and accept the Publishing Terms to continue."
- "Version name" text input present and empty
- "Publishing Terms" scrollable section present
- Checkbox labeled "I agree with the Publishing Terms." unchecked by default
- "Cancel" button enabled; "Continue" button disabled by default
- Closing via Cancel or ✕ does not publish anything

## Preconditions

- Logged in as User A on Agent A detail page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the 'Publish' button in Agent A's action bar | A modal dialog opens |
| 2 | Read the modal title | Title reads 'Publish version' |
| 3 | Inspect the stepper at the top of the modal | Three steps shown: Preparation (active/highlighted) → Validation → Publishing |
| 4 | Read the instruction text below the stepper | Text reads: 'Enter a version name and accept the Publishing Terms to continue.' |
| 5 | Locate the version name input field | A text input labeled 'Version name' is present and empty |
| 6 | Locate the Publishing Terms section | A section labeled 'Publishing Terms' with scrollable content is present |
| 7 | Verify the checkbox label and default state | Checkbox labeled 'I agree with the Publishing Terms.' is present and unchecked by default |
| 8 | Verify the Cancel button state | 'Cancel' button is visible and enabled |
| 9 | Verify the Continue button state with nothing filled | 'Continue' button is present but disabled (greyed out) |
| 10 | Click Cancel | Modal closes; no publish action occurs |
| 11 | Re-open the modal, then click the ✕ (close icon) | Modal closes; no publish action occurs |
| 12 | Navigate to Agents Studio and search for Agent A | Agent A is NOT present in Studio (no publish occurred from this incomplete flow) |

## Expected Final State

Agent A is NOT present in Studio (no publish occurred from this incomplete flow)

## Pass/Fail Criteria

PASS:
- Modal title is "Publish version"
- 3-step stepper with Preparation / Validation / Publishing is visible with Preparation active
- Instruction text, "Version name" field, "Publishing Terms" section, and "I agree with the Publishing Terms." checkbox are all present
- "Continue" button is disabled on modal open
- Closing via Cancel or ✕ does not publish the agent

FAIL:
- Modal title is different (e.g., "Publish Agent")
- Stepper is missing or shows wrong steps
- Checkbox or Continue button is missing
- Continue button is enabled before any input
- Closing modal triggers a publish action
- Page crash or modal fails to open
