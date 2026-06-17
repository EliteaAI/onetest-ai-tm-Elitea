---
id: ELITEA-0096
title: "Agent With Chat History — Switch Version Without LLM Override Error"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agent-publishing, feat:agents, feat:studio, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4934]
---
# ELITEA-0096: Agent With Chat History — Switch Version Without LLM Override Error

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that switching an agent version on the Agent page while the test chat already has message history does not trigger the spurious "LLM settings override" error.

**Coverage:**
- Version switch while test chat history is present
- Only a success notification appears on version switch — no LLM override error

## Preconditions

- Logged in to {{base_url}}
- Any agent with at least 2 saved versions open on the Agent page
- Chrome or Firefox, latest stable

## Test Data

- Agent: any existing agent with 2+ saved versions on the Agent page
- Chat message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any agent on the Agent page that has at least 2 saved versions (e.g. V1 and V2). | Agent page loads. The current active version is shown. |
| 2 | In the test chat panel, type `Hello` and send. | Agent responds. Chat history now exists. |
| 3 | Open the version selector and switch to a different version (e.g. V1). | V1 is selected as the active version. |
| 4 | Save the version change. | Version is saved. |
| 5 | Observe all notifications/toasts after saving. | Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear. |

## Expected Final State

Only a success toast appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear.

## Pass/Fail Criteria

**Pass:**
- Version is switched successfully
- Only a success message is shown
- No LLM settings override error appears

**Fail:**
- The error "LLM settings override is only allowed for published agents from agent studio" appears after switching the version — alone or alongside the success message
