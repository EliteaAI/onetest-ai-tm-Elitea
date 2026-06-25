---
id: ELITEA-0140
title: "Agent Dashboard and Search"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_agent_management.py:TestAgentList.test_agents_dashboard_loads
  - test_agent_management.py:TestAgentList.test_agent_search
  - test_agent_management.py:TestAgentList.test_agent_search_no_results
  - test_agent_management.py:TestAgentList.test_view_toggle_table_and_card
tags: []
requirements: []
---
# ELITEA-0140: Agent Dashboard and Search

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that Agents dashboard loads, displays agents correctly, and search functionality works properly.

**Coverage:**
- Agents dashboard page loads successfully
- Agent list displays created agents
- Search by agent name returns matching results
- Search with no matches shows empty state
- View toggle (table ↔ card view) works

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one agent exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Test user: alita@elitea.ai
- Non-existent search term for testing: zzzz_nonexistent_agent_12345

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | From the left sidebar, click 'Agents' to open the Agents dashboard. | Dashboard loads with 'Agents' header and a search input field visible at the top. |
| 2 | Look through the agent list to find your test agent (or any existing agent). | At least one agent is visible in the list. |
| 3 | Type the agent's name into the search input field at the top of the dashboard. | The list filters to show only agents matching the search term within 10 seconds. |
| 4 | Clear the search field and type 'zzzz_nonexistent_agent_12345'. | The list shows no results / empty state within a few seconds. |
| 5 | Clear the search. Look for a view toggle (table/card icons) near the top of the dashboard. Click the table view icon. | The view switches from card layout to a table layout. |
| 6 | Click the card view icon to switch back. | The view switches back to card layout. The 'Agents' header remains visible. |

## Expected Final State

The view switches back to card layout. The 'Agents' header remains visible.

## Pass/Fail Criteria

**Pass:**
- Dashboard loads with header and search
- Agent search finds matching agent
- No-results search shows empty state
- View toggle switches between table and card views
- No console errors or 5xx responses

**Fail:**
- Dashboard fails to load
- Search returns wrong results or times out
- View toggle buttons missing or non-functional
- 5xx server errors during search
