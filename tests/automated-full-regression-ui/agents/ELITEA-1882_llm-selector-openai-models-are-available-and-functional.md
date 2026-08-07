---
id: ELITEA-1882
title: "LLM selector — OpenAI models are available and functional (GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini)"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_llm_selector_openai_models.TestAgentLlmSelectorOpenaiModels.test_llm_selector_openai_models_are_available_and_functional
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1292
---

# ELITEA-1882: LLM selector — OpenAI models are available and functional (GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini)

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that all five specified OpenAI GPT models are present in the LLM selector dropdown, can be selected, saved, and are functional in the embedded chat panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.
- OpenAI models are configured in the platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Models to verify | GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini |
| Test message | Reply only with: CONFIRMED |
| Expected response | CONFIRMED |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Click the model selector dropdown | The model selector dropdown opens |
| 3 | Verify all five GPT models (GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini) are present in the dropdown | All five models are listed |
| 4 | Select "GPT-4.1" and click Save | Save completes successfully |
| 5 | Open the embedded chat panel and send: "Reply only with: CONFIRMED" | The message is sent |
| 6 | Verify the response contains "CONFIRMED" | The agent response contains "CONFIRMED" |
| 7 | Repeat steps 4–6 for "GPT-5 mini" | GPT-5 mini is selected, saved, and responds with "CONFIRMED" |
| 8 | Repeat steps 4–6 for "GPT-5.2" | GPT-5.2 is selected, saved, and responds with "CONFIRMED" |
| 9 | Repeat steps 4–6 for "GPT-5.4" | GPT-5.4 is selected, saved, and responds with "CONFIRMED" |
| 10 | Repeat steps 4–6 for "GPT-5.4-mini" | GPT-5.4-mini is selected, saved, and responds with "CONFIRMED" |

---

## Expected Final State

All five OpenAI GPT models are present in the dropdown, can be saved, and produce a valid response in the embedded chat.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All five GPT models are available and each responds correctly with "CONFIRMED".

**Fail:**
- Any step produces an error or unexpected result.
- One or more models are missing from the dropdown, or a model fails to produce the expected response.
