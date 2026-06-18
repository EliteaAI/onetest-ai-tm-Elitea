---
id: ELITEA-0220
title: "Project Default LLM Shown When Agent's LLM Is Unavailable in Current Project"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0220: Project Default LLM Shown When Agent's LLM Is Unavailable in Current Project

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a published agent's configured LLM is not available in the current project, the system falls back to showing the project's default LLM instead of displaying "None".

**Coverage:**
- "None" is never displayed as the LLM when a project default exists
- Fallback to project default LLM is applied automatically

## Preconditions

- A published agent (agentId=16) is configured with an LLM not available in the user's private project
- The private project has a default LLM set

## Test Data

Agent URL (private project context): {{base_url}}
Agent's configured LLM: one not present in private project
Expected fallback: project's default LLM (e.g. GPT-4.1 or as configured)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the private project where the agent's LLM is not available. | Project loaded. |
| 2 | Open the published agent in chat from this private project. | Chat interface displayed. |
| 3 | Observe the LLM section / model selector in the chat toolbar. | A valid model name (the project default) is shown — NOT 'None'. |
| 4 | Open Model Settings via the gear icon. | Settings panel shows a valid model configuration — not blank or 'None'. |

## Expected Final State

Settings panel shows a valid model configuration — not blank or 'None'.

## Pass/Fail Criteria

**Pass:**
- LLM selector shows the project's default model name, not "None"
- Model Settings panel is coherent with the fallback model

**Fail:**
- LLM selector or settings panel shows "None" where a project default exists
