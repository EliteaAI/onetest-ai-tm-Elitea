---
id: ELITEA-0147
title: "AI Validation Fallback — Agent-Level LLM Used When Project Low-Tier Field Is Empty"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4526]
---
# ELITEA-0147: AI Validation Fallback — Agent-Level LLM Used When Project Low-Tier Field Is Empty

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the project low-tier LLM field is empty, AI Validation falls back to the agent-level LLM — completing successfully when the agent LLM is valid and failing when the agent LLM has broken credentials.

**Coverage:**
- Project low-tier LLM field made empty (LLM unshared, removed, or cleared)
- UI shows low-tier field as empty
- Agent with broken LLM → validation does not complete (fallback also fails)
- Agent LLM switched to a correct one → validation completes (fallback to agent-level LLM works)

## Preconditions

- Logged in to {{base_url}}
- A project (public or team) with a low-tier LLM currently configured
- An LLM integration with broken credentials available
- A valid working LLM integration available
- Chrome or Firefox, latest stable

## Test Data

- Project: any project where you can edit LLM settings
- Low-tier LLM: make empty by unchecking "Shared" on the LLM, deleting it, or clearing the field
- Agent LLM (broken): an LLM integration with bad/expired credentials
- Agent LLM (correct): any valid working LLM integration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open project settings and make the low-tier LLM field empty (e.g. uncheck 'Shared' on the LLM, or remove/delete the LLM from the project). | Low-tier LLM field is displayed as empty in the project settings. |
| 2 | Open an agent in that project. In the agent LLM settings, set the LLM field to an integration with broken credentials. Save the changes. | Changes are saved. The agent LLM field shows the broken credentials integration. |
| 3 | Trigger Publish (AI Validation) on the agent. | Validation does not complete correctly — error expected, since no valid LLM is available (project low-tier is empty, agent LLM has broken credentials). |
| 4 | On the agent page, switch the LLM field to a correct, working LLM integration. Save the changes. | Changes are saved. The agent LLM field shows the correct integration. |
| 5 | Trigger Publish (AI Validation) again on the agent. | Validation completes and returns results — fallback to agent-level LLM works even when project low-tier is empty. |

## Expected Final State

Validation completes and returns results — fallback to agent-level LLM works even when project low-tier is empty.

## Pass/Fail Criteria

**Pass:**
- Step 1: low-tier field is visibly empty after the change
- Step 3: validation fails/does not complete (no usable LLM — broken agent LLM, empty project low-tier)
- Step 5: validation completes successfully using the valid agent-level LLM as fallback

**Fail:**
- Step 3: validation completes despite both the project low-tier being empty and the agent LLM being broken
- Step 5: validation still fails despite a valid agent-level LLM being set
