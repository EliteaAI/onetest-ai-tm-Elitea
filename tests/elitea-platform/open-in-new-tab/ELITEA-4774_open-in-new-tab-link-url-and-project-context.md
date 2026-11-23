---
id: ELITEA-4774
title: "Open in new tab: Link URL and project context"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, project-context, url, refresh, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4774: Open in new tab: Link URL and project context

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that links contain the current project ID, new tabs open in that project, and later project switching in the original tab does not affect them.

**Coverage:**
- Link URL format `/app/<projectId>/...`
- Project preserved in new tab, including after refresh

## Preconditions
- User has access to at least two projects: Project A and Project B.
- User is working in Project A; Project A has at least one Agent.

## Test Data
- Project A ID: `<projectA-id>`, Project B ID: `<projectB-id>`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Hover a **sidebar item** | Browser status bar shows `/app/<projectA-id>/...` |
| 2 | Hover an **agent card**, an **agent name** in table view, and **Run History** in the three-dot menu | Status bar shows `/app/<projectA-id>/...` with the entity path |
| 3 | Open the agent card in a new tab | New tab opens the agent in Project A (project selector shows Project A) |
| 4 | In the original tab, switch the project to Project B | Original tab shows Project B |
| 5 | Switch to the new tab and refresh it | New tab still shows Project A and the same agent |
| 6 | Open a sidebar link in a new tab from the original tab (now Project B) | New tab opens in Project B |

## Expected Final State
New tabs keep the project they were opened in; links always reflect the current project.

## Pass/Fail Criteria
- **Pass:** URLs contain the correct project ID and each new tab stays on its project after refresh.
- **Fail:** URL lacks/has a wrong project ID, or the new tab switches project after refresh.
