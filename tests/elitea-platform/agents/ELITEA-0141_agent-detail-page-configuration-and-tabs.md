---
id: ELITEA-0141
title: "Agent Detail Page - Configuration and Tabs"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_detail_page_loads
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_has_configuration_and_history_tabs
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_instructions_field
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_information_section
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_toolkits_section_visible
  - tests.ui.agents.test_agent_management.TestAgentConfiguration.test_internal_tools_enum_usage
tags: []
requirements: []
---
# ELITEA-0141: Agent Detail Page - Configuration and Tabs

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that Agent detail page loads correctly and displays all configuration sections (instructions, information, toolkits) and tabs (Configuration, History).

**Coverage:**
- Agent detail page loads successfully
- Configuration tab displays by default
- History tab is accessible
- Instructions field is visible and editable
- Information section shows agent metadata
- Toolkits section is visible

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one agent exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Test user: alita@elitea.ai
- Expected tabs on agent detail: Configuration, History
- Expected toolkit switches: Smart Tools Selection, Python sandbox, Data Analysis

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | From the left sidebar, click 'Agents'. On the Agents dashboard, click on any existing agent to open its detail page. | Agent detail page loads within 15 seconds. The Name field is visible and populated with the agent's name. |
| 2 | Verify the Name and Description fields are visible and filled with the agent's information. | Name field displays the agent's name. Description field shows the agent's description (may be empty if none was set). |
| 3 | Look at the tab bar near the top of the detail page. Verify both 'Configuration' and 'History' tabs are present. | Both 'Configuration' and 'History' tabs are visible and clickable. |
| 4 | Scroll down on the Configuration tab to find the Instructions field (labeled 'Guidelines for the AI agent'). | Instructions textarea is visible and contains text (or is empty if no instructions were set). |
| 5 | Look for the Information section on the page, which displays Agent ID and Version ID. | Agent ID and Version ID are displayed as non-empty values. |
| 6 | Scroll to the Toolkits section below the form fields. Verify the section heading and toggle switches. | Toolkits section is visible with at least 3 toggle switches (Smart Tools Selection, Python sandbox, Data Analysis). |

## Expected Final State

Toolkits section is visible with at least 3 toggle switches (Smart Tools Selection, Python sandbox, Data Analysis).

## Pass/Fail Criteria

**Pass:**
- All 6 steps pass
- Detail page loads within 15 seconds
- Name, description, and instructions match API-created values
- Both Configuration and History tabs visible
- Toolkits section displays at least 3 switches

**Fail:**
- Detail page fails to load or times out
- Name/description don't match API values
- Configuration or History tab missing
- Instructions field not visible or empty
- Toolkits section not found
