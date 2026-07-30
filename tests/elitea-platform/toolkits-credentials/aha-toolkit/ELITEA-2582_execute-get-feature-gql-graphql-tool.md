---
id: ELITEA-2582
title: "Execute get_feature_gql GraphQL tool"
priority: medium
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2582: Execute get_feature_gql GraphQL tool

**Module:** Toolkits · **Priority:** Medium · **Type:** Functional

**Objective:** Verify GraphQL tool executes and returns correct data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit configured with get_feature_gql tool
- Valid feature ID available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/
- Valid feature ID from Aha! instance

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select get_feature_gql tool | GraphQL tool executes successfully |
| 2 | Provide feature ID | Feature data is returned |
| 3 | Click RUN TOOL | Data is consistent with REST API response |
| 4 | Observe GraphQL response | Response format is correct |
| 5 | Compare with REST API response for same feature | Data matches between GraphQL and REST |

## Expected Final State

GraphQL tool executes successfully, feature data is returned, and data is consistent with REST API response.

## Pass/Fail Criteria

**Pass:**
- GraphQL tool executes successfully
- Feature data is returned
- Data is consistent with REST API response

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
