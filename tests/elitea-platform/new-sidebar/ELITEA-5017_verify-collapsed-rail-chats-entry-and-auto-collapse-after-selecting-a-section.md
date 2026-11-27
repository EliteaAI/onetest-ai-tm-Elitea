---
id: ELITEA-5017
title: "Verify collapsed rail Chats entry, Explore in the rail and auto-collapse after selecting a section"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7564]
---
# ELITEA-5017: Verify collapsed rail Chats entry, Explore in the rail and auto-collapse after selecting a section

## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has several chats
- **Spec conflict to confirm:** #7564 says selecting an Explore section collapses the sidebar automatically; #7560 says the sidebar is collapsed only by the user. Steps 1–2 follow #7564 — update them once the product owner confirms.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With the sidebar expanded, open **Explore** and select any section | The section page opens and the sidebar collapses automatically |
| 2 | Open **Explore** from the collapsed rail and select another section | The list opens next to the rail; the selected page opens and the sidebar stays collapsed |
| 3 | Look at the collapsed rail | A compact **Chats** entry is shown, without chat names or folders |
| 4 | Click the **Chats** entry | The sidebar expands and shows the chat history; no chat is opened or highlighted; the current page doesn't change |
| 5 | Collapse and expand the sidebar with the existing control | It toggles without navigation; the history scroll position and group/folder expansion are kept |
| 6 | Ctrl/Cmd-click a section in **Explore** while the sidebar is expanded | The section opens in a new tab; the current tab's sidebar stays expanded |

## Expected Final State

The user is on the last selected section page and no chat is selected.

## Pass/Fail Criteria

**Pass:**
- Selecting a section in the same tab collapses the sidebar (per the confirmed spec)
- Explore works from the rail; the Chats entry expands the sidebar without opening a chat
- Toggling never navigates and keeps the history state

**Fail:**
- The sidebar state after selecting a section contradicts the confirmed spec
- The rail has no Chats entry, or the entry opens or selects a chat
- Opening a section in a new tab changes the current tab's sidebar
