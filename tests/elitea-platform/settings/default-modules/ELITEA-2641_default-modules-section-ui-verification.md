---
id: ELITEA-2641
title: "Default Modules Section UI Verification"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2641: Default Modules Section UI Verification

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Default Modules section is visible under Settings → General with the correct table structure, all 10 modules displayed with proper names, descriptions, and toggle switches for Chats and Agents columns.

**Coverage:**
- Default Modules section visibility in Settings → General
- Table structure with Module, Chats, and Agents columns
- All 10 modules displayed with correct names and descriptions
- Toggle switches present for each module/column combination

## Preconditions

- Logged into {{base_url}}
- User has access to project Settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Expected modules:
1. Image Creation - Enable AI-powered image generation capabilities
2. Data Analysis - Enable data analysis capabilities
3. Agent & Pipeline Builder - Create and update agents and pipelines directly from chat
4. Skill Builder - Create and update skills from chat using internal Elitea MCP tools
5. Project Context Builder - Create and update project context from chat using internal Elitea MCP tools
6. Ask User - Let the agent pause and ask a clarifying question when uncertain
7. Planner - Enable managing and tracking todo items for task planning
8. Python Sandbox - Enable Python code execution in a secure sandbox
9. Swarm Mode - Enable swarm-style multi-agent collaboration
10. Smart Tools Selection - Reduces token usage by using meta-tools instead of binding all tools directly

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings from the sidebar. | Settings page loads successfully. |
| 2 | Click on "General" under the PROJECT section. | General settings page is displayed. |
| 3 | Locate the "Default Modules" section on the page. | Default Modules section is visible as a collapsible panel. |
| 4 | Expand the Default Modules section if collapsed. | Section expands showing a table with module configurations. |
| 5 | Verify the table header columns. | Table has exactly 3 columns: "Module", "Chats", "Agents". |
| 6 | Count the number of module rows in the table. | Exactly 10 module rows are displayed. |
| 7 | Verify each module name matches the expected list. | All 10 modules are present with correct names: Image Creation, Data Analysis, Agent & Pipeline Builder, Skill Builder, Project Context Builder, Ask User, Planner, Python Sandbox, Swarm Mode, Smart Tools Selection. |
| 8 | Verify each module has a description text below the name. | Each module row shows a descriptive help text explaining the module's purpose. |
| 9 | Verify toggle switches in Chats column. | Each module row has a toggle switch in the Chats column, disabled by default (toggle is in OFF position). |
| 10 | Verify toggle switches in Agents column. | Each module row has a toggle switch in the Agents column, disabled by default (toggle is in OFF position). |

## Expected Final State

Default Modules section is fully visible with all 10 modules, each having toggle switches for both Chats and Agents columns.

## Pass/Fail Criteria

**Pass:**
- Default Modules section is visible under Settings → General
- Table has exactly 3 columns (Module, Chats, Agents)
- All 10 modules are displayed with correct names and descriptions
- Each module has functional toggle switches for both columns

**Fail:**
- Default Modules section is missing or not accessible
- Table structure is incorrect (wrong columns or missing columns)
- Any module is missing or has incorrect name/description
- Toggle switches are missing for any module/column combination
