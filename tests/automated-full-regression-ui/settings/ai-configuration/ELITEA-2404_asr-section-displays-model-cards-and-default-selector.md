---
id: ELITEA-2404
title: "ASR section displays model cards and default selector"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2404: ASR section displays model cards and default selector

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that ASR section displays model cards and default selector. Success is confirmed when click the selector — verify a dropdown of available asr models appears.

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
| 2 | Locate the Speech Recognition (ASR) section | Action completes without error and produces the expected UI state. |
| 3 | Verify at least one model card is shown with: model name and status badge | Condition holds as described. |
| 4 | Verify the "Default ASR model" selector shows a non-empty value | Condition holds as described. |
| 5 | Click the selector — verify a dropdown of available ASR models appears | Control responds; expected next state is shown. |

---

## Expected Final State

Click the selector — verify a dropdown of available ASR models appears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: ASR section displays model cards and default selector.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
