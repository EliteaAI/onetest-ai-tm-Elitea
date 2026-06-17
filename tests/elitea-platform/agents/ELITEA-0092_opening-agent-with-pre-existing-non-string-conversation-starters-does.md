---
id: ELITEA-0092
title: "Opening agent with pre-existing non-string conversation_starters does not crash the UI"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [rca:missing-functionality, rca:data-quality, nfr:validation, feat:agents, eng:backend, eng:api, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4933]
---
# ELITEA-0092: Opening agent with pre-existing non-string conversation_starters does not crash the UI

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the frontend handles agents containing non-string `conversation_starters` values (persisted before the fix) gracefully — without a full-page crash or `TypeError: s.trim is not a function`.

**Coverage:**
- Agent detail modal opens without crashing when `conversation_starters` contains null, integer, or object values
- No `TypeError: s.trim is not a function` or uncaught JS exception in browser console
- Non-string items are silently excluded or replaced with an empty state
- Page remains fully interactive after opening the modal

## Preconditions

- User is logged in at {{base_url}}
- An agent named "FE error 4933" exists in the project with `conversation_starters: [null, 42, {}, "valid starter"]` — pre-seeded directly into the database or created via API before the fix was applied (bypassing frontend validation)
- No existing console errors before the test begins

## Test Data

**Pre-seeded agent payload** (used to create the corrupted agent via direct DB or pre-fix API call):
```json
{
  "name": "FE error 4933",
  "description": "desc",
  "type": "interface",
  "webhook_secret": null,
  "versions": [
    {
      "name": "base",
      "tags": [],
      "instructions": "",
      "variables": [],
      "tools": [],
      "llm_settings": {
        "max_tokens": -1,
        "temperature": 0.6,
        "reasoning_effort": "medium",
        "model_name": "gpt-5.2",
        "model_project_id": 1
      },
      "conversation_starters": [null, 42, {}, "valid starter"],
      "agent_type": "openai",
      "welcome_message": "",
      "meta": {
        "step_limit": 25
      }
    }
  ]
}
```
Agent name: `"FE error 4933"`
Expected corrupted field: `conversation_starters: [null, 42, {}, "valid starter"]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section from the left sidebar. | Agents list page loads. All agents are listed without errors. |
| 2 | Locate the agent named 'FE error 4933' in the list. | Agent card or row is visible in the list. |
| 3 | Click on the agent 'FE error 4933' to open its detail modal or configuration page. | The agent detail view or modal opens. The page does NOT go blank or display a full-page white-screen error. |
| 4 | Observe the browser errors. | No `TypeError: s.trim is not a function` or any uncaught exception appears in the console. |
| 5 | Scroll to the Conversation Starters section inside the agent detail view. | The section renders. Non-string items (null, 42, {}) are either silently excluded or shown as an empty/placeholder state. The valid string 'valid starter' may still appear. |
| 6 | Interact with other sections of the agent detail view (e.g., Instructions, LLM Settings). | All other sections are fully interactive. The page is stable and responsive. |

## Expected Final State

All other sections are fully interactive. The page is stable and responsive.

## Pass/Fail Criteria

**Pass:**
- Agent detail modal/page opens without any crash
- No `TypeError: s.trim is not a function` in the browser console
- Page is fully interactive after opening
- Non-string conversation starters are handled gracefully (excluded or empty state shown)

**Fail:**
- White-screen / full-page crash occurs after clicking the agent
- `TypeError: s.trim is not a function` or equivalent uncaught JS error appears in console
- The entire application becomes unresponsive
