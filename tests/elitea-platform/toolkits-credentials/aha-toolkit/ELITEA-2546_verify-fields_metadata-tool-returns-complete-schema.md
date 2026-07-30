---
id: ELITEA-2546
title: "Verify fields_metadata tool returns complete schema"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2546: Verify fields_metadata tool returns complete schema

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify fields_metadata tool returns complete field schema

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with fields_metadata tool

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select fields_metadata tool | Tool executes successfully |
| 2 | Provide record type parameter | Complete field schema is returned |
| 3 | Click RUN TOOL | All field types and properties are included |
| 4 | Observe response | Step completes successfully |
| 5 | Verify schema completeness | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Complete field schema is returned
- All field types and properties are included

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
