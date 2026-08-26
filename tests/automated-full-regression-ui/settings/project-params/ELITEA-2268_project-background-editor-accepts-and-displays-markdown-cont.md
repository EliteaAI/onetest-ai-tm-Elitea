---
id: ELITEA-2268
title: "Project Background editor accepts and displays markdown content"
priority: medium
type: functional
module: settings-project-params
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_project_context_markdown_editor.TestProjectContextMarkdownEditor.test_project_context_markdown_editor_and_preview
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1799"
---

# ELITEA-2268: Project Background editor accepts and displays markdown content

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Project Background editor accepts and displays markdown content. Success is confirmed when verify the raw markdown source is shown in the editor.

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
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Click inside the Project Background editor | Control responds; expected next state is shown. |
| 3 | Enter markdown content with headings, bullet points, and plain text | Field accepts the input and displays the entered value. |
| 4 | Verify the editor shows line numbers alongside the content | Condition holds as described. |
| 5 | Verify the content is editable inline (not read-only) | Condition holds as described. |
| 6 | Click the preview (eye) icon | Control responds; expected next state is shown. |
| 7 | Verify the content renders as formatted markdown in preview mode | Condition holds as described. |
| 8 | Click the code view (`</>`) icon | Control responds; expected next state is shown. |
| 9 | Verify the raw markdown source is shown in the editor | Condition holds as described. |

---

## Expected Final State

Verify the raw markdown source is shown in the editor.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Project Background editor accepts and displays markdown content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
