---
id: ELITEA-2001
title: "Build with AI — generation failure shows error and allows retry"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-2001: Build with AI — generation failure shows error and allows retry

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that when the skill draft generation fails (e.g., network error, service unavailable), a clear error message is shown in the modal, the original prompt is preserved, and the user can retry generation successfully.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The Build with AI modal is open with a natural-language description entered.
- A method to simulate or trigger a generation failure is available (e.g., network interruption, service unavailable condition).

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | Any valid prompt text |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Build with AI modal | The modal opens with the prompt input field |
| 2 | Enter a natural-language prompt | The input field accepts and displays the prompt |
| 3 | Simulate or trigger a generation failure (e.g., network interruption, service unavailable) | The generation request fails |
| 4 | Verify a clear error message is displayed in the modal | An error message is visible in the modal |
| 5 | Verify the previously entered natural-language prompt is still present in the input field | The original prompt text is preserved in the input field |
| 6 | Click the retry/Generate button again | The generation is retried |
| 7 | Verify the generation is retried and (if service recovers) a draft is returned | A skill draft is generated and the review form is displayed |

---

## Expected Final State

After a generation failure, the error is shown and the prompt is preserved. After retrying (with service recovered), a skill draft is successfully generated and shown in the review form.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Error message is shown, prompt is preserved, and retry produces a successful draft generation.

**Fail:**
- Any step produces an error or unexpected result.
- No error message is shown on failure, the prompt is cleared, or the retry button is not available.
