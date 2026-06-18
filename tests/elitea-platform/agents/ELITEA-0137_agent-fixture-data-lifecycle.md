---
id: ELITEA-0137
title: "Agent Fixture Data Lifecycle"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_agent_management.py:TestAgentIsolation.test_fixture_creates_fresh_agent
test_agent_management.py:TestAgentIsolation.test_fixture_cleanup_cycle
tags: []
requirements: []
---
# ELITEA-0137: Agent Fixture Data Lifecycle

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pytest fixture behavior for agent test data: fresh creation and cleanup.

**Coverage:**
- Fixture creates fresh agent for each test
- Fixture cleanup cycle (create → use → delete)

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Agent name prefix for testing: autotest_
- Cleanup cycle agent name: autotest_cleanup_cycle

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from the sidebar. Click 'Create Agent' to create a new agent with a name starting with 'autotest_' (e.g., 'autotest_lifecycle_test'). | A new agent is created with a valid ID and appears on the Agents dashboard. |
| 2 | Open the newly created agent's detail page from the dashboard. | The detail page loads. The Name field displays the agent name starting with 'autotest_'. |
| 3 | Verify the agent has an Agent ID displayed in the Information section. | The Agent ID is displayed and is a non-empty value. |
| 4 | Create another agent named 'autotest_cleanup_cycle'. | Agent is created successfully. |
| 5 | Go back to the Agents dashboard. Search for 'autotest_cleanup_cycle' to verify it appears in the list. | The agent appears in the search results. |
| 6 | Delete the 'autotest_cleanup_cycle' agent (via three-dot menu > Delete). Refresh the dashboard and search again. | The agent no longer appears in the dashboard after deletion and refresh. |

## Expected Final State

The agent no longer appears in the dashboard after deletion and refresh.

## Pass/Fail Criteria

**Pass:**
- Fixture creates agent with "autotest_" prefix name
- Agent ID matches between fixture and detail page
- Create → list → verify → delete → verify cycle completes
- No orphaned test data after cleanup

**Fail:**
- Fixture fails to create agent
- Agent ID mismatch between fixture and UI
- Delete does not remove agent from API list
- Orphaned agents left after test
