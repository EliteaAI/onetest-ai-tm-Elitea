---
id: ELITEA-0534
title: "Cross-scope — Agents: edit last message and re-submit"
priority: critical
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0534: Cross-scope — Agents: edit last message and re-submit

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the edit-and-resubmit feature works correctly in Agent chat context.

**Coverage:**
- Edit icon present on last user message in Agent chat
- Edit mode opens inline
- Save and apply triggers agent re-execution with updated input
- Cancel discards changes

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- An Agent is configured and accessible
- At least one user-assistant exchange exists in the Agent chat

## Test Data

- Agent: any available Agent
- Original message: "List 3 programming languages"
- Edited message: "List 3 databases"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to an Agent. Send "List 3 programming languages" and wait for the response. | Agent responds with programming languages. |
| 2 | Verify the Edit icon is present on the last user message. Click it. | Edit mode opens inline with original content pre-loaded. Cancel and Save and apply buttons visible. |
| 3 | Change text to "List 3 databases" and click "Save and apply". | Agent re-executes with the updated input. Loading state is shown. |
| 4 | Verify the new response. | Response mentions databases (not programming languages). Previous response is replaced. |

## Expected Final State

Response mentions databases (not programming languages). Previous response is replaced.

## Pass/Fail Criteria

**Pass:**
- Edit feature works identically in Agent context
- Agent re-executes based on updated input
- Previous response is replaced

**Fail:**
- Edit icon missing in Agent chat
- Agent does not re-execute
- Feature behaves differently than in Chat Conversations
