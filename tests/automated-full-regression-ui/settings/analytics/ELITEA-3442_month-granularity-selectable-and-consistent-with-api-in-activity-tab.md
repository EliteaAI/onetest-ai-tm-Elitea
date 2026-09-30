---
id: ELITEA-3442
title: "\"Month\" Granularity Is Selectable in Activity Tab and Matches API Behavior"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [feat:monitoring, nfr:data-visualization, story:5110, regression]
requirements: [EliteaAI/elitea_issues#6801]
---
# ELITEA-3442: "Month" Granularity Is Selectable in Activity Tab and Matches API Behavior

**Module:** Settings → Analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the "Month" granularity option is present and selectable in the Team Analytics → Activity tab's granularity dropdown, and that selecting it sends `granularity=month` and renders data grouped by month, consistent with calling the API directly — regression check for #6801, which is already fixed via [EliteaUI#1107](https://github.com/EliteaAI/EliteaUI/pull/1107) (merged). This case exists to verify the fix actually landed correctly, not to assume it did.

**Coverage:** Regression — [EliteaAI/elitea_issues#6801](https://github.com/EliteaAI/elitea_issues/issues/6801), fix [EliteaUI#1107](https://github.com/EliteaAI/EliteaUI/pull/1107).

## Preconditions

- A project with Team Analytics enabled and activity spanning at least 2 calendar months
- Ability to call the underlying Activity API endpoint directly with `granularity=month` for comparison

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Team Analytics → Activity tab. | Page loads. |
| 2 | Open the granularity/interval selector dropdown. | Dropdown opens showing available options. |
| 3 | Confirm "Month" is present and selectable in the list. | "Month" option is visible and clickable (not missing, as it was pre-fix). |
| 4 | Select "Month". | The Activity tab re-renders with data grouped by calendar month. |
| 5 | Call the Activity API endpoint directly with `granularity=month` for the same date range and project. | API response returns monthly-grouped data. |
| 6 | Compare the UI's monthly totals/rows against the direct API response from step 5. | Values match — the UI selection produces the same grouping and totals as the API. |

## Expected Final State

The "Month" granularity option is available and selectable in the UI, and produces results identical to calling the API directly with `granularity=month`.

## Pass/Fail Criteria

**Pass:**
- "Month" is present in the dropdown and selectable (step 3)
- UI output after selecting "Month" matches the direct API response (step 6)

**Fail:**
- "Month" is missing/unselectable in the UI (regression of #6801), or its output diverges from the API's `granularity=month` response
