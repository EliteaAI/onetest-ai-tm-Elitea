---
id: ELITEA-4738
title: "Preview/Edit switch and Instructions actions have consistent labels, tooltips, and keyboard access"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4738: Preview/Edit switch and Instructions actions have consistent labels, tooltips, and keyboard access

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the mode switch and the Edit-mode actions are clearly labeled, are the same for agents and skills, can be used from the keyboard, and display correctly in all themes and viewports.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" and skill "qa-7377-skill" exist.

---

## Test Data

| Field | Value |
|-------|-------|
| Entities | Agent "QA-7377 Agent"; skill "qa-7377-skill" |
| Expected accessible names | "Preview mode", "Edit mode" |
| Expected tooltips | "Copy to clipboard", "Full screen view" |
| Themes | Light, Dark |
| Viewports | 1280×720, 1920×1080 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent" and check the switch in DevTools | The switch is clearly labeled Preview / Edit, and the accessible names are "Preview mode" and "Edit mode" |
| 2 | Open "qa-7377-skill" and check the same | The labels, icons and accessible names are the same as on the agent |
| 3 | On the agent, press Tab to move focus to the switch | A visible focus ring is shown |
| 4 | Press Enter, then Space, on each mode option | The mode changes, and `aria-pressed="true"` moves to the active option |
| 5 | In Edit, press Tab to reach Copy to clipboard and Full Screen, and activate each with Enter | Each has a visible focus ring and works from the keyboard. The tooltips read "Copy to clipboard" and "Full screen view" |
| 6 | Repeat steps 3–5 on the skill | The results are the same |
| 7 | Check the controls in light and dark themes, at 1280×720 and at 1920×1080 | The controls are readable, have enough contrast, and do not overlap or cut off |

---

## Expected Final State

No data is changed.

---

## Pass/Fail Criteria

**Pass:**
- Labels, tooltips and keyboard behavior are the same for agents and skills, and are accessible in every theme and viewport.

**Fail:**
- A control is missing its label or tooltip, cannot be reached or used from the keyboard, or displays incorrectly in any theme or viewport.

---

## Notes

- At authoring time, the skill switch used an eye icon and a code icon with the aria-labels "Preview mode" and "Edit mode".
