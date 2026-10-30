---
id: ELITEA-1880
title: "LLM selector: Change model, verify settings dialog, test Anthropic and OpenAI providers"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1880: LLM selector: Change model, verify settings dialog, test Anthropic and OpenAI providers

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the LLM selector allows changing models, that the settings dialog shows appropriate fields for the selected model, that model selection persists after save and reload, and that both Anthropic and OpenAI model providers are available and functional in the embedded chat panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.
- Both Anthropic and OpenAI models are configured in the platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Anthropic models to verify | Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5 |
| OpenAI models to verify | GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini |
| Test message | Reply only with: CONFIRMED |
| Expected response | CONFIRMED |

---

## Steps

### Part 1: Model Selector and Settings Dialog Verification

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Note the currently selected model | The current model name is recorded |
| 3 | Click the model selector dropdown | The model selector dropdown opens |
| 4 | Choose a different model from the dropdown | The new model name is shown in the selector |
| 5 | Verify the selector displays the newly chosen model | The selector shows the selected model name |
| 6 | Click the Settings (⚙️) icon | The settings dialog opens |
| 7 | Verify the settings dialog shows appropriate fields: Reasoning slider (Low, Medium, High) + Max Completion Tokens (Auto/Custom) for standard models | The settings dialog displays the expected fields for the selected model type |
| 8 | Close the settings dialog | Settings dialog closes |

### Part 2: Test Anthropic Models

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Open the model selector and verify Anthropic models are present: Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5 | All three Anthropic models are listed in the dropdown |
| 10 | Select "Claude 4.5 Sonnet" and click Save | Save completes successfully |
| 11 | Open the embedded chat panel and send: "Reply only with: CONFIRMED" | The message is sent |
| 12 | Verify the response contains "CONFIRMED" | The agent response contains "CONFIRMED" |
| 13 | Select "Claude 4.6 Sonnet", Save, and send the test message | Claude 4.6 Sonnet responds with "CONFIRMED" |
| 14 | Select "Claude Haiku 4.5", Save, and send the test message | Claude Haiku 4.5 responds with "CONFIRMED" |

### Part 3: Test OpenAI Models

| # | Action | Expected Result |
|---|--------|-----------------|
| 15 | Open the model selector and verify OpenAI models are present: GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini | All five OpenAI models are listed in the dropdown |
| 16 | Select "GPT-4.1", Save, and send the test message | GPT-4.1 responds with "CONFIRMED" |
| 17 | Select "GPT-5 mini", Save, and send the test message | GPT-5 mini responds with "CONFIRMED" |
| 18 | Select "GPT-5.2", Save, and send the test message | GPT-5.2 responds with "CONFIRMED" |

### Part 4: Verify Model Selection Persistence

| # | Action | Expected Result |
|---|--------|-----------------|
| 19 | Note the last model selected (GPT-5.2) | Model name is recorded |
| 20 | Reload the page | The page reloads |
| 21 | Verify the model selector shows "GPT-5.2" (the last selected model) | The selector displays "GPT-5.2" |

---

## Expected Final State

- Model selector allows changing between Anthropic and OpenAI models.
- Settings dialog displays appropriate fields for the selected model.
- All three Anthropic models (Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5) are available and functional.
- All five OpenAI models (GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini) are available and functional.
- Last selected model (GPT-5.2) persists after page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Model selector dropdown opens and allows selection.
- Settings dialog opens and shows correct fields for the model type.
- All Anthropic models are present and respond correctly with "CONFIRMED".
- All OpenAI models are present and respond correctly with "CONFIRMED".
- Model selection persists after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- Model selector does not work correctly or settings dialog shows wrong fields.
- One or more Anthropic or OpenAI models are missing from the dropdown.
- Any model fails to produce the expected "CONFIRMED" response.
- Model selection does not persist after reload.

---

## Notes

**Source functional tests:** ELITEA-1880, ELITEA-1881, ELITEA-1882

**Regression rationale:** Consolidates LLM selector functionality testing across both major model providers (Anthropic and OpenAI) into a single comprehensive test. All key validations and checkpoints from the original three tests are preserved:
- ELITEA-1880: Model selector UI, settings dialog, and persistence
- ELITEA-1881: Anthropic models availability and functionality
- ELITEA-1882: OpenAI models availability and functionality

**Selected checkpoints:**
- Model selector dropdown functionality
- Settings dialog displays correct fields
- All Anthropic models (3) are available and functional
- All OpenAI models (5) are available and functional
- Model selection persists after page reload

**Testing strategy:** Tests representative models from each provider to verify availability and functionality without exhaustively testing every single model variant, focusing on confirming the selector mechanism and provider integration work correctly.
