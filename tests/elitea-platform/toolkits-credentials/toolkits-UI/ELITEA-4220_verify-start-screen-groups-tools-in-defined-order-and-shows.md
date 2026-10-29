---
id: ELITEA-4220
title: "Verify start screen groups tools in defined order and shows flat list without groups"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4220: Verify start screen groups tools in defined order and shows flat list without groups

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkits exist: Jira (`Jira_Management`), GitHub, Confluence (with tool groups) and an MCP toolkit (no tool groups)

## Test Data

| Toolkit | Tool groups |
|---------|-------------|
| `Jira_Management` (Jira) | Yes |
| GitHub | Yes |
| Confluence | Yes |
| MCP toolkit | No |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `Jira_Management` and note the order of group headers in the TOOLS section. | The group order is recorded. |
| 2 | Click **Test**. | The start screen opens. |
| 3 | Look at the group headers on the start screen. | Headers are shown in uppercase and in the same order as in the TOOLS section. |
| 4 | Look at the tools inside each group. | Tools are sorted alphabetically, ignoring case. |
| 5 | Repeat steps 1–4 for the GitHub and Confluence toolkits. | Group order matches the TOOLS section and tools are sorted alphabetically in each group. |
| 6 | Open the MCP toolkit and click **Test**. | Tools are shown as one flat list without group headers. |

## Expected Final State

Start-screen tools are grouped in the same order as the TOOLS section and sorted alphabetically. Toolkits without groups show a flat list.

## Pass/Fail Criteria

**Pass:**
- The group order matches the TOOLS section for every grouped toolkit
- Tools are sorted alphabetically in each group
- The MCP toolkit shows a flat list without headers

**Fail:**
- Group order differs from the TOOLS section
- Tools are not sorted alphabetically
- Group headers appear for a toolkit without groups, or tools are missing
