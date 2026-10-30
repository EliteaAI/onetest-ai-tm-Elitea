---
id: ELITEA-4218
title: "Verify Test page start screen lists all tools and opens the form for the picked tool"
priority: critical
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4218: Verify Test page start screen lists all tools and opens the form for the picked tool

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkits exist with valid credentials: Jira (`Jira_Management`), GitHub, Confluence, MCP
- The Jira credential has access to project `TEST`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/toolkits` |
| Main toolkit | `Jira_Management` |
| Tool to pick | `Search using JQL` |
| JQL | `project = TEST ORDER BY created DESC` |
| Other toolkits | GitHub, Confluence, MCP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the `Jira_Management` toolkit and note the enabled tools in the TOOLS section. | The list of enabled tools is recorded. |
| 2 | Click **Test**. | The Test page opens with a start screen instead of the old empty "Choose a tool from the list" state. |
| 3 | Look at the start screen. | It shows the hint "Pick a tool to configure its parameters and run a test.", a "Search tools..." field and the tools as clickable buttons. |
| 4 | Compare the tool buttons with the tools recorded in step 1. | Every enabled tool is shown once; no tool is missing or duplicated. |
| 5 | Click `Search using JQL`. | The start screen closes; the parameters form for `Search using JQL` opens and the **Tool** selector shows `Search using JQL`. |
| 6 | Enter JQL `project = TEST ORDER BY created DESC` and run the test. | The test runs and the result appears in the Results panel. |
| 7 | Repeat steps 1–5 for the GitHub, Confluence and MCP toolkits, picking any tool. | For each toolkit the start screen lists all enabled tools and picking a tool opens its parameters form. |

## Expected Final State

The Test page opens on the start screen. Picking a tool opens its parameters form, and the test runs successfully.

## Pass/Fail Criteria

**Pass:**
- The start screen shows the hint, the search field and all enabled tools
- Picking a tool opens the correct parameters form with the Tool selector set
- The test run returns a result

**Fail:**
- The old empty state is shown
- A tool is missing or duplicated on the start screen
- Picking a tool opens the wrong form, no form, or an error
