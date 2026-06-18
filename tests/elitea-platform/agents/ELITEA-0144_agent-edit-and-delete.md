---
id: ELITEA-0144
title: "Agent Edit and Delete"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_agent_management.py:TestAgentActions.test_edit_agent_name
test_agent_management.py:TestAgentActions.test_edit_agent_description
test_agent_management.py:TestAgentActions.test_delete_agent_via_api
test_agent_management.py:TestAgentActions.test_delete_agent_via_ui_menu
tags: []
requirements: []
---
# ELITEA-0144: Agent Edit and Delete

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can edit agent properties (name, description) and delete agents via UI menu and API.

## Preconditions

- User logged into Elitea
- Test agent exists

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open agent detail page | Configuration tab visible |
| ? | Edit agent name, save | Name updated in UI |
| ? | Edit description, save | Description updated |
| ? | Delete via UI menu | Agent removed from list |

## Expected Final State

Agent removed from list

## Pass/Fail Criteria

**Pass:**
- Name edits persist
- Description edits persist
- Delete via UI removes agent
- Delete via API removes agent

**Fail:**
- Edits don't save
- Deleted agent still visible
