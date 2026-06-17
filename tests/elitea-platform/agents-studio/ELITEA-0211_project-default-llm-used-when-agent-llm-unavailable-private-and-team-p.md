---
id: ELITEA-0211
title: "Project Default LLM Used When Agent LLM Unavailable — Private and Team Project"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0211: Project Default LLM Used When Agent LLM Unavailable — Private and Team Project

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a published agent's configured LLM is unavailable in the accessing project, the project's default LLM is displayed — not "None" — for both private and team project contexts.

**Coverage:**
- Private project context: fallback to project default LLM
- Team project context: fallback to project default LLM

## Preconditions

- Published agent (agentId=16) uses an LLM not provisioned in the test projects
- Both private and team projects have a default LLM configured

## Test Data

Scenario A: Private project — Agent LLM not available — Expected: project default (e.g. GPT-4.1)
Scenario B: Team project — Agent LLM not available — Expected: team project default

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the published agent from the private project (agent's LLM not available). | LLM section shows the project's default LLM (e.g. GPT-4.1), not 'None'. |
| 2 | Open the same published agent from a team project (agent's LLM not available). | LLM section shows the team project's default LLM, not 'None'. |
| 3 | In both scenarios, confirm the agent can be interacted with using the fallback LLM. | Messages can be sent and responses received. |

## Expected Final State

Messages can be sent and responses received.

## Pass/Fail Criteria

**Pass:**
- Neither private nor team project context shows "None"
- Fallback project default LLM is displayed and functional in both cases

**Fail:**
- "None" appears in either context when a project default LLM is available
