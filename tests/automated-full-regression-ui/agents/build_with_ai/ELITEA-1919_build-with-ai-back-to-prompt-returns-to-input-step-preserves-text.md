---
id: ELITEA-1919
title: "Build with AI — \"Back to prompt\" returns to input step and preserves prompt text"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1919: Build with AI — "Back to prompt" returns to input step and preserves prompt text

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Back to prompt" control in the review/edit step returns the user to the prompt input step with the previously entered description preserved, and no draft data leaks into the prompt step UI.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| Original prompt text | The natural-language description submitted to generate the draft |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft and enter the review/edit form | The review/edit form is displayed |
| 2 | Click "Back to prompt" (or equivalent back control) | The modal navigates back |
| 3 | Verify the modal returns to the prompt input step | The prompt input step is displayed |
| 4 | Verify the previously entered natural-language description is still present in the input field | The original prompt text is present and unchanged in the input field |
| 5 | Verify no draft data leaks into the prompt step UI | The prompt step only shows the input field and action buttons — no review form fields or generated content is visible |

---

## Expected Final State

The modal is on the prompt input step, showing the preserved original prompt text without any draft data visible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The modal returns to the prompt step with the original prompt preserved and no draft data leaking into the UI.

**Fail:**
- Any step produces an error or unexpected result.
- The prompt text is lost, or generated draft data is visible in the prompt step UI.
