---
id: ELITEA-2393
title: "OpenAI Template tab loads code template content"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2393: OpenAI Template tab loads code template content

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that OpenAI Template tab loads code template content. Success is confirmed when click back to "ai configuration" tab — verify the integrations content returns.

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
| 2 | Click the "OpenAI Template" tab | Control responds; expected next state is shown. |
| 3 | Verify the tab becomes active | Condition holds as described. |
| 4 | Verify the content area shows a code template (non-empty) | Condition holds as described. |
| 5 | Click back to "AI Configuration" tab — verify the integrations content returns | Control responds; expected next state is shown. |

---

## Expected Final State

Click back to "AI Configuration" tab — verify the integrations content returns.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: OpenAI Template tab loads code template content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
