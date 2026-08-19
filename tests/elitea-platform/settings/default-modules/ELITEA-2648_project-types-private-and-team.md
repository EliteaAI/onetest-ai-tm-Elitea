---
id: ELITEA-2648
title: "Default Modules in Private and Team Projects"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:projects, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2648: Default Modules in Private and Team Projects

**Module:** Default Modules · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Default Modules section is available and functions correctly in both Private projects and Team projects, with independent configurations per project.

**Coverage:**
- Default Modules section visible in Private project settings
- Default Modules section visible in Team project settings
- Each project maintains independent module default configuration
- Changes in one project do not affect another project

## Preconditions

- Logged into {{base_url}}
- User has access to at least one Private project
- User has access to at least one Team project with settings permissions
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Private project: "Private"
Team project: Any accessible Team project with edit permissions

Configuration for Private project:
- Enable: Image Creation, Data Analysis (Chats)

Configuration for Team project:
- Enable: Python Sandbox, Swarm Mode (Agents)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select the Private project from the project selector. | Private project context is active. |
| 2 | Navigate to Settings → General. | Settings page opens. |
| 3 | Verify Default Modules section is present. | Default Modules section is visible and accessible. |
| 4 | Enable Image Creation and Data Analysis for Chats column. | Toggles switch to ON. |
| 5 | Verify other modules remain OFF. | All other toggles are OFF. |
| 6 | Create a new Chat in Private project. | Chat created with Image Creation and Data Analysis enabled. |
| 7 | Switch to a Team project using the project selector. | Team project context is active. |
| 8 | Navigate to Settings → General. | Settings page opens for Team project. |
| 9 | Verify Default Modules section is present. | Default Modules section is visible and accessible. |
| 10 | Verify Team project has independent default state (likely all OFF if unconfigured). | Team project module defaults are independent from Private project. |
| 11 | Enable Python Sandbox and Swarm Mode for Agents column. | Toggles switch to ON. |
| 12 | Create a new Agent in Team project. | Agent created with Python Sandbox and Swarm Mode enabled. |
| 13 | Switch back to Private project. | Private project context is active. |
| 14 | Navigate to Settings → General → Default Modules. | Settings page opens. |
| 15 | Verify Private project settings are unchanged. | Image Creation and Data Analysis still ON for Chats. Python Sandbox and Swarm Mode still OFF. |
| 16 | Create a new Chat in Private project. | Chat created with Private project defaults (Image Creation, Data Analysis enabled). |

## Expected Final State

- Private project has its own Default Modules configuration (Image Creation, Data Analysis for Chats)
- Team project has its own independent configuration (Python Sandbox, Swarm Mode for Agents)
- Each project's entities use their respective project defaults

## Pass/Fail Criteria

**Pass:**
- Default Modules section is accessible in both Private and Team projects
- Each project maintains independent module configuration
- Changes in one project do not affect another project
- New entities in each project use the correct project-specific defaults

**Fail:**
- Default Modules section missing in Private or Team project
- Project configurations are linked or shared unexpectedly
- Changes in one project affect another project
- New entities do not use project-specific defaults
