---
id: ELITEA-1152
title: "get_pull_request tool works in Pipeline Toolkit Node"
priority: high
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1152: get_pull_request tool works in Pipeline Toolkit Node

**Module:** Ado Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Pipeline with ADO toolkit node can execute get_pull_request and pass description field to subsequent nodes.

**Coverage:**
- Pipeline with ADO toolkit node can execute get_pull_request
- Description field is retrieved successfully
- Description field is passed correctly to subsequent nodes
- Pipeline execution completes without errors

## Preconditions

- User authenticated with valid account
- ADO Toolkit configured and available
- Test ADO repository accessible with PRs
- Environment: {{base_url}}

## Test Data

- Pipeline name: [Test Pipeline with ADO Toolkit Node]
- Toolkit: ADO Toolkit
- Tool: get_pull_request
- PR ID: [Valid PR ID with description]
- Pipeline structure: ADO toolkit node → Output node (to verify data flow)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from sidebar | Pipelines page loads |
| 2 | Create a new pipeline or open existing test pipeline | Pipeline opens |
| 3 | Add a Toolkit Node to the pipeline | Toolkit node added |
| 4 | Configure the Toolkit Node to use ADO Toolkit | ADO Toolkit selected |
| 5 | Select get_pull_request tool in the node configuration | Tool selected |
| 6 | Configure tool parameters (PR ID as input variable or hardcoded) | Parameters configured |
| 7 | Add an Output Node or subsequent node that receives toolkit node output | Output node added |
| 8 | Save the pipeline | Pipeline saved |
| 9 | Execute the pipeline with valid PR ID | Pipeline executes |
| 10 | Verify pipeline execution completes successfully | Execution completes |
| 11 | Review the output from ADO toolkit node | Output displayed |
| 12 | Verify description field is present in toolkit node output | Description present |
| 13 | Verify subsequent node receives description field data | Data passed |

## Expected Final State

Data passed

## Pass/Fail Criteria

**Pass:**
- Pipeline executes successfully
- ADO toolkit node completes get_pull_request call
- Description field is present in toolkit node output
- Description field data is passed to subsequent nodes
- No execution errors in pipeline

**Fail:**
- Pipeline execution fails
- ADO toolkit node fails to execute get_pull_request
- Description field is missing from output
- Data is not passed to subsequent nodes
- Execution errors appear
