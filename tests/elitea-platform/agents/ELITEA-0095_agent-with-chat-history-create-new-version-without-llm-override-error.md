---
id: ELITEA-0095
title: "Agent With Chat History — Create New Version Without LLM Override Error"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, feat:studio, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4934]
---
# ELITEA-0095: Agent With Chat History — Create New Version Without LLM Override Error

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that creating a new agent version while the test chat already has message history does not trigger the spurious "LLM settings override" error.

**Coverage:**
- New version creation while test chat history is present
- Only a success notification appears on version creation — no LLM override error

## Preconditions

- Logged in to {{base_url}}
- Any agent open in Agent Studio
- Chrome or Firefox, latest stable

## Test Data

- Agent: any existing agent in Agent Studio
- Chat message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any agent in Agent Studio. | Agent configuration page loads. |
| 2 | In the test chat panel, type `Hello` and send. | Agent responds. Chat history now exists. |
| 3 | Click 'Create Version' (or equivalent version creation control). | Version creation dialog or action is triggered. |
| 4 | Confirm version creation. | New version is saved. |
| 5 | Observe all notifications/toasts after the version is created. | Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear. |

## Expected Final State

Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear.

## Pass/Fail Criteria

**Pass:**
- New version is created successfully
- Only a success message is shown
- No LLM settings override error appears

**Fail:**
- The error "LLM settings override is only allowed for published agents from agent studio" appears after version creation — alone or alongside the success message
