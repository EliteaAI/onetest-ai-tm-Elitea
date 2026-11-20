---
id: ELITEA-4767
title: "Open in new tab: Sidebar items and Settings"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, sidebar, navigation, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4767: Open in new tab: Sidebar items and Settings

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that every sidebar navigation item and Settings is a real link that can be opened in a new tab via the browser's native "Open link in new tab" option.

**Coverage:**
- Sidebar items: Chats, Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Credentials, Applications, Artifacts
- Settings → Project General
- Original tab is not affected

## Preconditions
- User is logged in to ELITEA and has access to at least one project.
- The user is on any page of the project (e.g., Chats).

## Test Data
- Project: any project the user can access (`<projectId>`)

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Right-click **Chats** in the sidebar | Browser's native context menu appears with "Open link in new tab" |
| 2 | Select "Open link in new tab" | New tab opens the Chats page of the same project; original tab stays on the current page |
| 3 | Repeat steps 1–2 for **Agents** | New tab opens the Agents list |
| 4 | Repeat steps 1–2 for **Pipelines** | New tab opens the Pipelines list |
| 5 | Repeat steps 1–2 for **Skills** | New tab opens the Skills list |
| 6 | Repeat steps 1–2 for **Toolkits & Indexes** | New tab opens the Toolkits & Indexes list |
| 7 | Repeat steps 1–2 for **MCPs** | New tab opens the MCPs list |
| 8 | Repeat steps 1–2 for **Credentials** | New tab opens the Credentials list |
| 9 | Repeat steps 1–2 for **Applications** | New tab opens the Applications list |
| 10 | Repeat steps 1–2 for **Artifacts** | New tab opens the Artifacts page |
| 11 | Right-click **Settings** in the sidebar and select "Open link in new tab" | New tab opens Settings › Project General |
| 12 | Switch back to the original tab | Original tab is still on the page it was on before step 1; no navigation happened |

## Expected Final State
All sidebar destinations and Settings open the correct pages in new tabs; the original tab is unchanged.

## Pass/Fail Criteria
- **Pass:** Every listed sidebar item shows the native "Open link in new tab" option and opens the correct page in a new tab.
- **Fail:** Any item lacks the option, opens the wrong page, shows an error, or changes the original tab.
