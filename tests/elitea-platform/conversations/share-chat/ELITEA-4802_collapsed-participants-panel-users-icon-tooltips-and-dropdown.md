---
id: ELITEA-4802
title: "Collapsed Participants panel users icon, tooltips and dropdown"
priority: medium
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4802: Collapsed Participants panel users icon, tooltips and dropdown

**Module:** conversations · **Priority:** medium · **Type:** functional

**Objective:** Verify the users icon of the collapsed Participants panel, the tooltip position of all collapsed icons and the users dropdown with the Share row.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Same chats as in the Users card case (C1 only the owner, C2 5 selected people incl. User B); the Participants panel is collapsed.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open C2, then C1 | The users icon has a count badge (same count as the card) or a lock badge for Only You |
| 2 | Hover each icon of the collapsed panel (users, agents, pipelines, skills, toolkits, MCPs) | Tooltips open to the left of the icons, inside the window |
| 3 | On C2 click the users icon | Dropdown to the left: summary line ("5 users · 🔗 n"), Everyone, people (rules of the Users dropdown), a divider and the row "Share" that never overlaps a user row |
| 4 | Click Share as User A, then as User B | User A: the Share Chat window opens. User B: no window; the link is copied with a toast |
| 5 | On C1 click the users icon | Only the summary line and "Share" |
| 6 | With the dropdown open, open Export from the chat menu | The dropdown closes, or the modal is shown above it |

---

## Expected Final State

The collapsed panel gives the same information and actions as the Users card.

---

## Notes

- Steps 3 and 6 depend on #7715.
