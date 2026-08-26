---
id: ELITEA-2266
title: "Project Context page loads with correct layout and components"
priority: medium
type: functional
module: settings-project-params
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_project_context_page_layout.TestProjectContextPageLayout.test_project_context_page_layout
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1799"
---

# ELITEA-2266: Project Context page loads with correct layout and components

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Project Context page loads with correct layout and components. Success is confirmed when verify the page does not show any errors or permanent loading state.

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
| 2 | Verify the page header shows "Project Context" | Condition holds as described. |
| 3 | Verify the Project Context toggle card is shown at the top with: | Condition holds as described. |
| 4 | Title "Project Context" | Action completes without error and produces the expected UI state. |
| 5 | Description text explaining the feature | Action completes without error and produces the expected UI state. |
| 6 | An ON/OFF toggle (enabled by default) | Action completes without error and produces the expected UI state. |
| 7 | Verify the "Project Background" section is shown below with: | Condition holds as described. |
| 8 | Section title "Project Background" | Action completes without error and produces the expected UI state. |
| 9 | Subtitle describing what to include (goals, terminology, workflows, constraints) | Action completes without error and produces the expected UI state. |
| 10 | A "Build with AI" button | Action completes without error and produces the expected UI state. |
| 11 | An upload file icon button | Action completes without error and produces the expected UI state. |
| 12 | A code view (`</>`) icon button | Action completes without error and produces the expected UI state. |
| 13 | A preview (eye) icon button | Action completes without error and produces the expected UI state. |
| 14 | A code/markdown editor with line numbers | Action completes without error and produces the expected UI state. |
| 15 | Verify Save and Discard buttons are present at the bottom | Condition holds as described. |
| 16 | Verify the page does not show any errors or permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not show any errors or permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Project Context page loads with correct layout and components.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
