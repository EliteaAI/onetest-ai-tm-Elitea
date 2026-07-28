---
id: ELITEA-2496
title: "Verify all toolkit form fields render correctly"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2496: Verify all toolkit form fields render correctly

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all required form fields render correctly on the toolkit configuration page

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- New Aha! Toolkit configuration page is open

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Toolkit configuration page | "Toolkit Name" text input field is visible and editable |
| 2 | Verify "Toolkit Name" field is present | "Description" text area field is visible and editable |
| 3 | Verify "Description" field is present | "Aha Configuration" dropdown is visible with placeholder or options |
| 4 | Verify "Aha Configuration" dropdown field is present | "Tools" section displays with multiple tool checkboxes |
| 5 | Verify "Tools" section with checkboxes is present | Both Form and Raw Json tabs are visible and clickable |
| 6 | Verify Form and Raw Json tabs are present | Step completes successfully |

## Expected Final State

"Toolkit Name" text input field is visible and editable

## Pass/Fail Criteria

**Pass:**
- "Toolkit Name" text input field is visible and editable
- "Description" text area field is visible and editable
- "Aha Configuration" dropdown is visible with placeholder or options
- "Tools" section displays with multiple tool checkboxes
- Both Form and Raw Json tabs are visible and clickable

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
