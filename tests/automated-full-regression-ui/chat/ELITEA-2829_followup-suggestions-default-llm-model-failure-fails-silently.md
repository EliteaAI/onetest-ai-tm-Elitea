---
id: ELITEA-2829
title: "Chat – Default Suggestion-Generation LLM Model Failing Does Not Surface an Error and Does Not Affect the Main Chat Response"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2829: Chat – Default Suggestion-Generation LLM Model Failing Does Not Surface an Error and Does Not Affect the Main Chat Response

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the default/fallback LLM model used internally for suggestion generation is unavailable, misconfigured, or otherwise not working (invalid credentials, deprecated model, provider outage), suggestion generation fails silently — no chip list, no error/toast — and the main chat response is completely unaffected.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Ability to configure the internal default suggestion-generation model to an invalid/unavailable state (e.g. invalid credentials, deprecated model ID, or a simulated provider outage) via test/admin configuration.

---

## Test Data

| Field | Value |
|-------|-------|
| Broken model config | Suggestion-generation model set to an invalid credential / deprecated model / simulated outage |
| Message | Any suggestion-eligible prompt |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Apply the broken suggestion-generation model configuration | Configuration is confirmed broken/invalid |
| 2 | Send the message and wait for the main AI response to complete | Main AI response completes normally with no visible impact |
| 3 | Observe the composer area for any suggestion UI, error, or toast | No chip list, error message, or toast appears |
| 4 | Restore a working suggestion-generation model configuration and repeat the same message | Suggestions render normally, confirming the earlier failure was isolated to the broken model |

---

## Expected Final State

A broken suggestion-generation model produces a fully silent no-op for suggestions while leaving the main chat experience completely intact.

---

## Pass/Fail Criteria

**Pass:**
- Main AI response is delivered normally despite the broken suggestion model.
- No error, toast, or partial chip UI appears.
- Restoring a working model configuration restores normal suggestion behavior.

**Fail:**
- The main AI response is delayed, errored, or otherwise affected by the broken suggestion model.
- Any error/toast/partial UI is shown to the user as a result of the broken suggestion model.
