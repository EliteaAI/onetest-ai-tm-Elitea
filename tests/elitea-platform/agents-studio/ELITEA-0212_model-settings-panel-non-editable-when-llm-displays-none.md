---
id: ELITEA-0212
title: "Model Settings Panel Non-Editable When LLM Displays None"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0212: Model Settings Panel Non-Editable When LLM Displays None

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the LLM selector shows "None" (no valid model resolved), the Model Settings panel is disabled and does not allow configuration changes.

**Coverage:**
- Settings panel is read-only when no LLM is set
- No indeterminate state (e.g. reasoning toggle active with no model context)

## Preconditions

- Reproducing condition: agent's LLM is not available in the current project, causing "None" to display
- Access via private project where agent's LLM is not provisioned

## Test Data

Agent URL: {{base_url}} accessed from private project without agent's LLM

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the published agent from a private project where the LLM is not available. | LLM section shows 'None'. |
| 2 | Attempt to open or interact with the Model Settings panel (gear icon or settings controls). | Panel should be disabled or inaccessible. |
| 3 | Verify that no toggles or inputs within the settings panel are active. | All controls are greyed out or unresponsive. |

## Expected Final State

All controls are greyed out or unresponsive.

## Pass/Fail Criteria

**Pass:**
- Settings panel is non-editable when LLM is "None"
- No settings can be modified in this state

**Fail:**
- Settings panel remains active and editable when LLM is "None"
- Reasoning toggle or other controls remain interactive without a valid LLM context
