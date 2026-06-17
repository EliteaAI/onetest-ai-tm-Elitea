---
id: ELITEA-0148
title: "Agent With Chat History — Save Agent Changes Without LLM Override Error"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, feat:studio, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4934]
---
# ELITEA-0148: Agent With Chat History — Save Agent Changes Without LLM Override Error

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that saving an agent configuration change in Agent Studio while the test chat contains message history does not trigger the spurious "LLM settings override" error.

**Coverage:**
- Agent configuration change (e.g. instructions, temperature) saved while test chat has history
- Only a success notification appears — no LLM override error appears alongside or instead

## Preconditions

- Logged in to {{base_url}}
- Any agent open in Agent Studio
- Chrome or Firefox, latest stable

## Test Data

- Agent: any existing agent in Agent Studio
- Config change: any minor edit, e.g. add a space to System Instructions
- Chat message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any agent in Agent Studio. | Agent configuration page loads. |
| 2 | In the test chat panel, type `Hello` and send. | Agent responds. Chat history now exists. |
| 3 | Make a minor change to the agent config (e.g. add a space to System Instructions). | Change is reflected in the editor. Save button becomes active. |
| 4 | Click Save. | Save request is submitted. |
| 5 | Observe all notifications/toasts after saving. | Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear. |

## Expected Final State

Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear.

## Pass/Fail Criteria

**Pass:**
- Save completes with only a success message
- No LLM settings override error appears at any point

**Fail:**
- The error "LLM settings override is only allowed for published agents from agent studio" appears — alone or alongside the success message
