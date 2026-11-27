---
id: ELITEA-4927
title: "New chat and Chats history in sidebar: create, search, folder, import and scroll"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4927: New chat and Chats history in sidebar: create, search, folder, import and scroll

## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has 30+ chats (enough to overflow the sidebar) and at least one chat folder
- A chat export file is available for import
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Viewport | 1366 × 768 |
| New chat message | `Regression sidebar chat` |
| Search text | Part of an existing chat name |
| Import file | A chat export file from the same environment |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Check the **+ New chat** button | It is a single button with no split/dropdown arrow and no list of other entity types |
| 2 | Open an existing chat, then click **+ New chat** | A new empty chat opens in the selected project |
| 3 | Send the new chat message from the Test Data | The chat appears in the sidebar Chats history |
| 4 | Check the Chats area | Only the selected project's chats and folders are listed, and the header has Search, Create folder and Import chat icons |
| 5 | Click **Search** and type the search text | The list filters to the matching chats, and clearing the search restores the list |
| 6 | Click **Create folder** and save a new folder | The folder appears in the Chats history |
| 7 | Click **Import chat** and import the file | The imported chat appears in the Chats history |
| 8 | Scroll down inside the Chats history to the end | Only the history scrolls, more chats load as you scroll, and the logo, project selector, + New chat, Artifacts, Explore and bottom row stay visible |

## Expected Final State

A new chat, a new folder and an imported chat exist in the selected project, and the history scrolls without hiding fixed areas.

## Pass/Fail Criteria

**Pass:**
- + New chat offers only chat creation, and the chat lands in the selected project's history
- Search, Create folder and Import chat work from the sidebar header
- The history scrolls independently and keeps loading, with header and bottom row visible

**Fail:**
- Other entity types are offered, or the chat goes to another project or doesn't appear
- Any header action is missing or broken
- The whole sidebar scrolls, chats stop loading, or the bottom row is hidden

## Notes

**Source functional tests:** ELITEA-4900, ELITEA-4901, ELITEA-4902
**Regression rationale:** Chat creation and history moved from the chat page into the sidebar; this is the most-used journey in the product.
**Selected checkpoints:** Single New chat button; chat created in project and listed; project-scoped list; Search; Create folder; Import; independent scroll with lazy loading.
**Cleanup:** Delete the new chat, imported chat and folder after the run.
