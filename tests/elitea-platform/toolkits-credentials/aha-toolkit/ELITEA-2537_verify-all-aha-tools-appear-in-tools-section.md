---
id: ELITEA-2537
title: "Verify all Aha! tools appear in TOOLS section"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2537: Verify all Aha! tools appear in TOOLS section

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify all Aha! tools appear in TOOLS section with checkboxes

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on New Aha! Toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to TOOLS section | All 30+ Aha! tools are listed |
| 2 | Scroll through all available tools | Each tool has a checkbox for selection |
| 3 | Verify each tool has a checkbox | Tools are organized logically |
| 4 | Count total number of tools | Step completes successfully |

## Expected Final State

All 30+ Aha! tools are listed

## Pass/Fail Criteria

**Pass:**
- All 30+ Aha! tools are listed
- Each tool has a checkbox for selection
- Tools are organized logically

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
