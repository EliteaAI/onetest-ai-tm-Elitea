---
id: ELITEA-2374
title: "DEPRECATED — Context management toggle enables and disables token fields"
priority: medium
type: functional
module: settings-user-profile
status: deprecated
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: [EliteaAI/elitea_issues#6898]
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_context_management_toggle_enables_disables_fields
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1241
---

# ELITEA-2374: DEPRECATED — Context management toggle enables and disables token fields

**Deprecation note (2026-11-12):** Per EliteaAI/elitea_issues#6898 AC4 ("togle was deleted"), the overarching Context Management on/off toggle this case tests no longer exists in the shipped UI. The Context window radio (Balanced/Full) and Automatic Summarization section are now always visible, not gated behind a toggle. This case's own steps were already stale even before AC4's removal (step 2/3 incorrectly describe "Context window toggle ... options Balanced and Full" and "Automatic Summarization toggle ... options Balanced and Full" — a copy/paste error, since Summarization never had Balanced/Full options). **No rewrite target identified; recommend formal deprecation in `index.json` and retirement of the linked automated test**, pending confirmation there is no replacement scenario worth automating (e.g., simply confirming no toggle exists — already covered by the new manual case ELITEA-4671 in this repo).

Original content retained below for reference only — do not execute.

---

~~**Objective:** Verify that Context management toggle enables and disables token fields. Success is confirmed when click the toggle back on — verify both fields and summarization become editable again.~~

---

## Preconditions (original, no longer applicable)

- User is logged in to the Elitea platform.

---

## Test Data (original, no longer applicable)

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps (original, no longer applicable)

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Verify the "Context window" toggle is present with options Balanced and Full | Condition holds as described. |
| 3 | Verify the "Automatic Summarization" toggle is present with options Balanced and Full | Condition holds as described. |

---

## Expected Final State (original, no longer applicable)

Click the toggle back ON — verify both fields and summarization become editable again.

---

## Pass/Fail Criteria (original, no longer applicable)

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Context management toggle enables and disables token fields.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
