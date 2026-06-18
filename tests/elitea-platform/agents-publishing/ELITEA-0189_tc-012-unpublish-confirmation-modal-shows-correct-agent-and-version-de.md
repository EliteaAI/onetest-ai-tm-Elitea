---
id: ELITEA-0189
title: "TC-012: Unpublish Confirmation Modal Shows Correct Agent and Version Details"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0189: TC-012: Unpublish Confirmation Modal Shows Correct Agent and Version Details

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify the unpublish confirmation modal renders all required contextual information before the action is committed, and that clicking Cancel does not unpublish anything.

Coverage:
- Warning icon present
- Agent name and version name shown in modal
- Impact text states agent removed from Studio and existing conversations blocked
- Cancel aborts without any change
- Confirm Unpublish triggers the action

## Preconditions

- Logged in as User A (owner)
- Agent A has a published version 'v2.0'
- Agent A is visible in Agents Studio

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A's published versions list | Published version 'v2.0' is listed with an 'Unpublish' option |
| 2 | Click 'Unpublish' on 'v2.0' | Confirmation modal opens |
| 3 | Check for a warning icon | A visual warning icon is visible |
| 4 | Read the agent name displayed in the modal | Agent A's name is shown |
| 5 | Read the version name displayed in the modal | 'v2.0' is shown as the version being unpublished |
| 6 | Read impact text | Text states: agent will be removed from Agents Studio AND existing conversations will be preserved but users cannot send new messages |
| 7 | Click 'Cancel' | Modal closes; Agent A v2.0 remains published; Agent A still appears in Agents Studio |
| 8 | Re-open unpublish modal and click 'Confirm Unpublish' | Unpublish proceeds; success notification shown; Agent A v2.0 removed from Studio |

## Expected Final State

Unpublish proceeds; success notification shown; Agent A v2.0 removed from Studio

## Pass/Fail Criteria

PASS:
- All required content is present in the unpublish confirmation modal
- Cancel aborts the action — agent remains published
- Confirm Unpublish executes the unpublish and shows success notification

FAIL:
- Modal is missing agent name, version name, warning icon, or impact text
- Agent is unpublished without a confirmation modal being shown
- Cancel button unpublishes the agent
