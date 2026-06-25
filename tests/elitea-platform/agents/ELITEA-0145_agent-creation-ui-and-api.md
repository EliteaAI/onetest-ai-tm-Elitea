---
id: ELITEA-0145
title: "Agent Creation - UI and API"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_agent_management.py:TestCreateAgent.test_create_agent_via_ui
  - test_agent_management.py:TestCreateAgent.test_create_agent_via_api_visible_in_ui
  - test_agent_management.py:TestCreateAgent.test_create_agent_required_fields_validation
tags: []
requirements: []
---
# ELITEA-0145: Agent Creation - UI and API

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can create agents via UI and API, with proper field validation.

## Preconditions

- User logged into Elitea
- Access to Agents dashboard

## Test Data

- URL: {{base_url}}
- Name: autotest_agent_<timestamp>

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Click 'Create Agent' button | Dialog opens with required fields |
| ? | Fill name and description, submit | Agent created, appears in list |
| ? | Create agent via API | Agent visible in UI immediately |

## Expected Final State

Agent visible in UI immediately

## Pass/Fail Criteria

**Pass:**
- Agent creation via UI succeeds
- API-created agents visible in UI
- Validation prevents empty required fields

**Fail:**
- Any 5xx errors
- Agent not visible after creation
- Invalid data accepted
