---
id: ELITEA-2325
title: "Guide tab displays explanatory documentation for each metric"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_guide_tab.TestAnalyticsGuideTab.test_guide_tab_metric_documentation
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1957"
---

# ELITEA-2325: Guide tab displays explanatory documentation for each metric

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Guide tab displays explanatory documentation for each metric. Success is confirmed when verify the guide content is readable and not truncated.

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
| 1 | Navigate to Settings → Analytics → Guide tab | Target page/section loads successfully. |
| 2 | Verify the tab loads a documentation/guide page (not blank) | Condition holds as described. |
| 3 | Verify the following sections are present: Overview Tab, with subsections: TEAM, AI ACTIVE, Adoption Rate, LLM CALLS | Condition holds as described. |
| 4 | Verify each metric section shows: description text, Calculation (highlighted in blue), Data source (highlighted in blue) | Condition holds as described. |
| 5 | Verify the Guide content is readable and not truncated | Condition holds as described. |

---

## Expected Final State

Verify the Guide content is readable and not truncated.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Guide tab displays explanatory documentation for each metric.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
