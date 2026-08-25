---
id: ELITEA-2756
title: "Applying wizard changes updates the Agent configuration correctly"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent with known current values for Name, Description, and Instructions is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Improve the agent name and description" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and note the current values for Name, Description, Instructions | Current values are recorded for comparison |
| 2 | Click "Edit with AI" and enter the test prompt | Prompt is accepted |
| 3 | Click "Generate Draft" and wait for completion | Wizard renders with suggestions |
| 4 | Step through the wizard leaving all suggestion checkboxes checked | All checkboxes remain in their default checked state |
| 5 | Navigate to the Summary step | The merged values (current + accepted suggestions) are displayed |
| 6 | Click the finalize/apply button | The modal closes without error |
| 7 | Observe the Agent configuration page | The page now shows the updated Name and Description values matching the accepted suggestions |
| 8 | Refresh the page | The updated values persist after reload |

## Expected Final State

The Agent's Name and Description reflect the applied AI suggestions, and the change is persisted server-side (survives refresh).

## Pass/Fail Criteria

**Pass:**
- Applied changes are visible immediately after closing the modal and remain after a page refresh

**Fail:**
- Changes are not applied, only partially applied, or revert after refresh
