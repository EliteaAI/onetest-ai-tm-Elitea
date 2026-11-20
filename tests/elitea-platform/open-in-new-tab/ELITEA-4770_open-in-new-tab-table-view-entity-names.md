---
id: ELITEA-4770
title: "Open in new tab: Table view entity names"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, table-view, list, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4770: Open in new tab: Table view entity names

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that entity names in table (list) view are real links that open the correct entity in a new tab for each entity type.

**Coverage:**
- Table view for Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Credentials, Applications
- Table state (sort, filters, page) is preserved

## Preconditions
- User is logged in.
- At least one entity of each type exists in the project.
- Table view is selected on each entity list page.

## Test Data
- One entity per type with a known name

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Agents** in table view; right-click an agent name → "Open link in new tab" | Native menu shows the option; new tab opens that agent with matching name/ID |
| 2 | Repeat for **Pipelines** | New tab opens the clicked pipeline |
| 3 | Repeat for **Skills** | New tab opens the clicked skill |
| 4 | Repeat for **Toolkits & Indexes** | New tab opens the clicked toolkit |
| 5 | Repeat for **MCPs** | New tab opens the clicked MCP |
| 6 | Repeat for **Credentials** | New tab opens the clicked credential |
| 7 | Repeat for **Applications** | New tab opens the clicked application |
| 8 | In any table, change the sort and apply a filter; open a name in a new tab; return to the original tab | Sort, filter, and page in the original tab are unchanged |

## Expected Final State
Table names behave as real links for all entity types; the original table state is preserved.

## Pass/Fail Criteria
- **Pass:** All 7 entity types open the correct entity from table view and the original table is unchanged.
- **Fail:** Any name lacks the option, opens a wrong entity, or the original table resets.
