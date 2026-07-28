---
id: ELITEA-2549
title: "Verify create_record_link tool links records"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2549: Verify create_record_link tool links records

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify create_record_link tool successfully links records

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with create_record_link tool
- Two valid record IDs are available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select create_record_link tool | Tool executes successfully |
| 2 | Provide source and target record IDs | Records are linked in Aha! |
| 3 | Click RUN TOOL | Response confirms link creation |
| 4 | Verify success response | Step completes successfully |
| 5 | Check records in Aha! to confirm link | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Records are linked in Aha!
- Response confirms link creation

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
