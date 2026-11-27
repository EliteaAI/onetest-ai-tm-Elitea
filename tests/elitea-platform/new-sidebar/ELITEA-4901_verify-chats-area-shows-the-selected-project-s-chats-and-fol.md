---
id: ELITEA-4901
title: "Verify Chats area shows the selected project's chats and folders with header actions"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4901: Verify Chats area shows the selected project's chats and folders with header actions


## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has at least two chats and one chat folder
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` | The **Chats** area is shown in the sidebar below Explore |
| 2 | Compare the chats and folders with the project's known chats | Only the selected project's accessible chats and folders are listed |
| 3 | Check the Chats header | **Search**, **Create folder** and **Import chat** icon buttons are next to the "Chats" label |
| 4 | Click **Search** and type part of a chat name | The list filters to the matching chats |
| 5 | Click **Create folder** | The new-folder flow starts as on dev |
| 6 | Click **Import chat** | The import dialog opens as on dev |

## Expected Final State

The Chats area lists the project's history, and the header actions work.

## Pass/Fail Criteria

**Pass:**
- The project's chats and folders are listed, and all three header actions work

**Fail:**
- Chats from other projects appear, or the project's chats are missing
- Any header action is missing or broken
