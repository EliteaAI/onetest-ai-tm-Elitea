---
id: ELITEA-4224
title: "Verify expanded sections and start screen display correctly in dark and light themes"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4224: Verify expanded sections and start screen display correctly in dark and light themes

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkit `Jira_Management` exists
- Access to the Figma design (Alita Project → Toolkit Test page)

## Test Data

| Theme | Pages |
|-------|-------|
| Dark | Toolkit details page, Test start screen |
| Light | Toolkit details page, Test start screen |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In **Settings**, switch to Dark theme. | The Dark theme is applied. |
| 2 | Open `Jira_Management`. | The expanded Configuration and TOOLS sections are readable, with correct colors. |
| 3 | Click **Test**. | The hint text, group labels, tool buttons and search field are readable and match the Figma design. |
| 4 | Hover over a tool button. | The hover color is applied and the label stays readable. |
| 5 | Switch to Light theme and repeat steps 2–4. | All elements are readable and match the Figma design in Light theme. |

## Expected Final State

The expanded sections and the start screen display correctly in both themes.

## Pass/Fail Criteria

**Pass:**
- All elements are readable in both themes and match Figma

**Fail:**
- Any element has low-contrast text, wrong colors, or no hover state in either theme
