---
id: ELITEA-4809
title: "Share Chat window layout, keyboard, themes and small screens"
priority: medium
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4809: Share Chat window layout, keyboard, themes and small screens

**Module:** conversations · **Priority:** medium · **Type:** functional

**Objective:** Verify the layout, keyboard use, theme colours and small-screen behaviour of the Share Chat window.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 with a long name, access for at least 15 people and at least 6 external links.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Share on Team, then on Externally | The window is 600 × 640 px on both tabs; header and tabs stay, only the area under the tabs scrolls; long names are cut with "…" |
| 2 | Make the browser shorter than 704 px | The window height is the screen height minus 64 px; the footer stays visible |
| 3 | Use only the keyboard: Tab, Enter/Space, Escape | Focus is visible and in a sensible order; Escape closes the dropdown first, then the window (with the unsaved warning if needed) |
| 4 | Switch between dark and light themes | "Remove access for all" and "Invite to project" use the Auxiliary text button colours with hover colour; the Expired badge is orange, text white in dark and #0E131D in light |
| 5 | Open the people dropdown near the bottom of the list | The dropdown floats over the window and is not clipped |

---

## Expected Final State

The window is usable on every screen size, by keyboard and in both themes.
