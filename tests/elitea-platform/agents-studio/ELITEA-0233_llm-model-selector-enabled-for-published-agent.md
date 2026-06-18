---
id: ELITEA-0233
title: "LLM Model Selector Enabled for Published Agent"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0233: LLM Model Selector Enabled for Published Agent

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the LLM model selector button is enabled and interactive in the chat toolbar when a user accesses a published Agent Studio agent.

**Coverage:**
- LLM model selector is not greyed out or disabled
- Control is clickable for published agents

## Preconditions

- Logged in to {{base_url}}
- A published Agent Studio agent exists (e.g. "Assistant for ELITEA Documentation", agentId=16)
- Agent is accessed via Agent Studio

## Test Data

Agent URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent Studio and open a published agent. | Agent detail page is displayed. |
| 2 | Start a new conversation with the agent. | Chat interface opens. |
| 3 | Observe the LLM model selector button in the chat toolbar (bottom of the chat input area). | The button showing the model name (e.g. 'Anthropic Claude 4.5 Sonnet') is visible. |
| 4 | Attempt to click the LLM model selector button. | Button responds to click — it is not greyed out, not disabled, and not locked. |

## Expected Final State

Button responds to click — it is not greyed out, not disabled, and not locked.

## Pass/Fail Criteria

**Pass:**
- LLM model selector button is clickable and not visually disabled
- No tooltip or label indicating "locked" or "read-only"

**Fail:**
- Button is greyed out, unresponsive, or shows a disabled state
- A lock icon or "disabled" visual indicator is present
