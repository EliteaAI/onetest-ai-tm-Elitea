---
id: ELITEA-4771
title: "Open in new tab: Three-dot menu Run History and Evaluate"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, three-dot-menu, run-history, evaluation, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4771: Open in new tab: Three-dot menu Run History and Evaluate

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that navigation items in the entity three-dot menu (Run History, Evaluate (Beta)) are links that open the correct destination in a new tab without triggering any action.

**Coverage:**
- Run History: Agent, Pipeline, Skill
- Evaluate (Beta): Agent, Pipeline
- No side effects in the original tab

## Preconditions
- User is logged in.
- An Agent, a Pipeline and a Skill exist (preferably with at least one run each).

## Test Data
- Agent `QA-Agent-NewTab`, Pipeline `QA-Pipeline-NewTab`, Skill `QA-Skill-NewTab`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the three-dot menu of the **Agent**; right-click **Run History** → "Open link in new tab" | New tab opens the Run History page of that agent |
| 2 | Open the three-dot menu of the **Pipeline**; right-click **Run History** → "Open link in new tab" | New tab opens the Run History page of that pipeline |
| 3 | Open the three-dot menu of the **Skill**; right-click **Run History** → "Open link in new tab" | New tab opens the Run History page of that skill |
| 4 | Open the three-dot menu of the **Agent**; right-click **Evaluate (Beta)** → "Open link in new tab" | New tab opens the Evaluate page of that agent |
| 5 | Open the three-dot menu of the **Pipeline**; right-click **Evaluate (Beta)** → "Open link in new tab" | New tab opens the Evaluate page of that pipeline |
| 6 | Return to the original tab after each step | Original page is unchanged; no run, evaluation or other action was started |

## Expected Final State
Menu navigation items open their destinations in new tabs with no side effects.

## Pass/Fail Criteria
- **Pass:** All 5 menu links open the correct page for the correct entity and nothing is triggered in the original tab.
- **Fail:** Missing option, wrong destination/entity, or an action is triggered.
