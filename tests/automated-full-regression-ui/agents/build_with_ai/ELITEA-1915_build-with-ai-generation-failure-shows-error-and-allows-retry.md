---
id: ELITEA-1915
title: "Build with AI — generation failure shows error and allows retry (Agent)"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1915: Build with AI — generation failure shows error and allows retry (Agent)

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that when agent draft generation fails, a clear error message is displayed, the previously entered prompt is preserved, and the user can retry generation from the same state.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The GenerateAgentModal is open with a prompt entered.
- A network or service failure condition can be triggered or simulated.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language prompt | Any valid description text |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and enter a natural-language description | The input field contains the entered description |
| 2 | Trigger or simulate a generation failure (e.g., network interruption) | The generation attempt fails |
| 3 | Verify a clear error message is displayed in the modal | An error message is displayed in the modal indicating generation failed |
| 4 | Verify the previously entered prompt is still present in the input field | The prompt text entered before the failure is still visible in the input field |
| 5 | Click the retry / "Generate agent" button | The generation is retried |
| 6 | Verify the generation is retried and (if service recovers) a draft is returned | If service recovers, the modal transitions to the review form with a generated draft |

---

## Expected Final State

After a generation failure, the error message is shown, the prompt is preserved, and the retry mechanism successfully initiates a new generation attempt.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Error message is displayed on failure, prompt is preserved, and retry is available and functional.

**Fail:**
- Any step produces an error or unexpected result.
- No error message is shown, the prompt is lost after failure, or there is no retry option.
