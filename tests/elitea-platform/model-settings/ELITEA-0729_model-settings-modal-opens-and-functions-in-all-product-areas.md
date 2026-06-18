---
id: ELITEA-0729
title: "Model Settings Modal Opens and Functions in All Product Areas"
priority: critical
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0729: Model Settings Modal Opens and Functions in All Product Areas

**Module:** Model Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the model settings modal loads successfully and model selection works end-to-end across Chat, Agents, and Pipelines after the Vision capability indicator enhancement.

**Coverage:**
- Model settings modal opens without errors in Chat
- Model settings modal opens without errors in Agents
- Model settings modal opens without errors in Pipelines (LLM node)
- Model selection changes are applied correctly in all contexts
- All previously available models remain visible and selectable

## Preconditions

- Logged into {{base_url}}
- User has access to Chat, Agents, and Pipelines features
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has multiple models available with different capabilities

## Test Data

- Test models: GPT-4 Vision, GPT-3.5-turbo, Claude 3 Opus, GPT-5.2
- Test agent: any existing agent with editable model configuration
- Test pipeline: any existing pipeline with an LLM node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Click the model selector dropdown at the top of the chat interface. | Model dropdown opens without errors. All available models are listed. |
| 2 | Select a different model from the list (e.g., switch from GPT-3.5 to GPT-4 Vision). Close the dropdown. | Model selection is applied. The selected model name is displayed in the dropdown button. |
| 3 | Send a test message in Chat (e.g., 'Hello'). | Response is received from the newly selected model. |
| 4 | Navigate to Agents. Open or create an agent. Go to the agent's model configuration section. | Agent model configuration loads without errors. Model settings are visible. |
| 5 | Change the agent's model to a different one. Save the agent. Test the agent by sending a message. | Agent saves successfully. Agent responds using the newly configured model. |
| 6 | Navigate to Pipelines. Open or create a pipeline. Add or edit an LLM node. Open the LLM node's model configuration. | LLM node model configuration opens without errors. Model selection is available. |
| 7 | Change the LLM node's model. Save the pipeline. Execute the pipeline. | Pipeline saves successfully. Pipeline executes and the LLM node uses the configured model. |

## Expected Final State

Pipeline saves successfully. Pipeline executes and the LLM node uses the configured model.

## Pass/Fail Criteria

**Pass:**
- Model settings modal/dropdown opens in all three contexts (Chat, Agents, Pipelines)
- Model selection changes are successfully applied in all contexts
- All test interactions complete without errors
- Previously available models remain visible and selectable

**Fail:**
- Model settings modal fails to open in any context
- Model selection does not apply or reverts unexpectedly
- Errors occur during model configuration or usage
- Some previously available models are missing from the list
