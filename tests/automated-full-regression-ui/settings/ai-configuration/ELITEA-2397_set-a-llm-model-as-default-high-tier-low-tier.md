---
id: ELITEA-2397
title: "Set a LLM model as Default / High-tier / Low-tier"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2397: Set a LLM model as Default / High-tier / Low-tier

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Set a LLM model as Default / High-tier / Low-tier. Success is confirmed when verify that selected default model is used whe nstarting a chat.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | Target page/section loads successfully. |
| 2 | In the LLM Models section, click the "Default" tier dropdown selector | Action completes without error and produces the expected UI state. |
| 3 | Select a different model from the list | Control responds; expected next state is shown. |
| 4 | Verify the selector updates to show the newly selected model | Condition holds as described. |
| 5 | Verify the corresponding model card gains a "Default" badge | Condition holds as described. |
| 6 | Verify the previously default model card no longer shows the "Default" badge | Condition holds as described. |
| 7 | Navigate to new chat and start a conversation | Target page/section loads successfully. |
| 8 | Verify that selected default model is used whe nstarting a chat | Condition holds as described. |
| 9 | Repeat steps 2–8 for High-tier and Low-tier selectors | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Repeat steps 2–8 for High-tier and Low-tier selectors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Set a LLM model as Default / High-tier / Low-tier.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
