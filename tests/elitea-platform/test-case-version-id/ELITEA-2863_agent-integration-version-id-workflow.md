---
id: ELITEA-2863
title: "Agent Integration - Version ID Workflow"
priority: medium
type: integration
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, agent, version-id, integration, workflow]
requirements: [EL-6085, EL-6340]
---
# ELITEA-2863: Agent Integration - Version ID Workflow

**Module:** QTest Toolkit · **Priority:** Medium · **Type:** Integration

**Objective:** Verify that an agent can successfully use the QTest toolkit to retrieve test case versions and update a test run with a specific version ID.

**Coverage:**
- Agent can call Get Test Case Versions tool
- Agent can extract correct version ID from response
- Agent can call Update Test Run Status with version ID
- Error messages are actionable for agent self-correction

## Preconditions

- Logged in to {{base_url}}
- Agent configured with QTest toolkit enabled
- Test case exists with multiple versions (e.g., 1.0, 2.0, 3.0, 4.0)
- Test run available for updating

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/agents` |
| Agent | Agent with QTest toolkit |
| Test Case ID | Test case with multiple versions |
| Target Version | 2.0 |
| Test Run ID | Valid test run ID |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents section. | Agents list displays. |
| 2 | Open the agent with QTest toolkit. | Agent chat interface opens. |
| 3 | Send prompt: "Get the versions for test case ID [X]". | Agent calls Get Test Case Versions tool. |
| 4 | Verify agent receives version list. | Agent shows versions with IDs and names. |
| 5 | Send prompt: "Update test run [Y] status to Passed for version 2.0". | Agent processes the request. |
| 6 | Observe agent's tool calls. | Agent extracts version ID for "2.0" from previous response. |
| 7 | Verify agent calls Update Test Run Status with version ID. | Tool call includes correct numeric version ID. |
| 8 | Verify update succeeds. | Success message returned. |
| 9 | Check QTest to confirm update on correct version. | Result associated with version 2.0. |
| 10 | Test error handling: Send prompt with wrong version. | Agent receives error with valid alternatives. |
| 11 | Verify agent can self-correct using error message. | Agent uses error info to retry with valid ID. |

## Expected Final State

Agent successfully completes the version lookup and update workflow, demonstrating full integration capability.

## Pass/Fail Criteria

**Pass:**
- Agent successfully calls Get Test Case Versions
- Agent correctly extracts version ID for requested version name
- Agent calls Update Test Run Status with correct version ID
- Update succeeds and is reflected in QTest
- Error messages enable agent self-correction

**Fail:**
- Agent cannot call Get Test Case Versions
- Agent fails to map version name to ID
- Agent sends incorrect version ID
- Update fails despite correct workflow
- Error messages not actionable for agent
