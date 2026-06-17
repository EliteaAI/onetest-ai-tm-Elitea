---
id: ELITEA-0146
title: "AI Validation Uses Project-Level Low-Tier LLM — Broken Agent LLM Does Not Block Validation"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4526]
---
# ELITEA-0146: AI Validation Uses Project-Level Low-Tier LLM — Broken Agent LLM Does Not Block Validation

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Publish AI Validation uses the project-level low-tier LLM model, so that a broken or misconfigured agent-level LLM does not prevent validation from completing.

**Coverage:**
- Project configured with a correct low-tier LLM
- Agent configured with a broken/misconfigured LLM
- AI validation completes successfully using the project-level low-tier model
- Switching the project low-tier to a correct model unblocks validation

## Preconditions

- Logged in to {{base_url}}
- Access to project-level LLM settings
- A broken/invalid LLM integration available (bad credentials or unstable endpoint)
- Chrome or Firefox, latest stable

## Test Data

- Project low-tier LLM: initially set to a broken/invalid LLM integration
- Agent LLM: any (not relevant, preferable broken llm — validation should not use it)
- Correct low-tier LLM: a valid working LLM integration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open project settings and set the low-tier LLM to a broken/invalid LLM integration. | Low-tier field shows the broken LLM. |
| 2 | Open any agent in that project and trigger Publish (AI Validation). | Validation does not complete — fails due to the broken project-level low-tier model. |
| 3 | Go back to project settings and switch the low-tier LLM to a correct, working LLM integration. | Low-tier field shows the correct LLM. |
| 4 | Trigger Publish (AI Validation) again on the same agent. | Validation completes successfully and returns results. |

## Expected Final State

Validation completes successfully and returns results.

## Pass/Fail Criteria

**Pass:**
- Step 2: validation fails/does not complete when low-tier LLM is broken (confirms validation uses the project-level model)
- Step 4: validation completes successfully after switching to a correct project-level low-tier LLM

**Fail:**
- Step 2: validation completes despite the broken project-level low-tier (meaning it used the agent-level LLM instead)
- Step 4: validation still fails despite the correct low-tier LLM being set
