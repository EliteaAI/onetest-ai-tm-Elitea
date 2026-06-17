---
id: ELITEA-0226
title: "Model Settings Dialog Opens via Gear Icon for Published Agent"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0226: Model Settings Dialog Opens via Gear Icon for Published Agent

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the gear icon next to the model name in the chat toolbar opens the Model Settings dialog for published agents.

**Coverage:**
- Gear icon is clickable
- Model Settings dialog displays Creativity and Max Completion Tokens controls

## Preconditions

- Published agent is open in chat at {{base_url}}

## Test Data

Agent: Assistant for ELITEA Documentation (agentId=16)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a published agent in chat. | Chat toolbar is visible with model name and gear icon (⚙). |
| 2 | Click the gear icon (⚙) next to the model name. | A dialog titled 'Model settings' opens. |
| 3 | Observe the dialog contents. | Dialog shows: Creativity slider (1–5), Max Completion Tokens section (Auto/Custom radio), Max Tokens input, Remaining Tokens, Reset to defaults, Cancel, Apply buttons. |

## Expected Final State

Dialog shows: Creativity slider (1–5), Max Completion Tokens section (Auto/Custom radio), Max Tokens input, Remaining Tokens, Reset to defaults, Cancel, Apply buttons.

## Pass/Fail Criteria

**Pass:**
- Dialog opens without errors
- All expected controls (Creativity, Max Completion Tokens, Apply, Cancel, Reset) are present

**Fail:**
- Gear icon is unresponsive or disabled
- Dialog does not open or opens blank
