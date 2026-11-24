---
id: ELITEA-4796
title: "Share Chat Team tab people picker dropdown and Invite to project"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4796: Share Chat Team tab people picker dropdown and Invite to project

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify the people picker of the Team tab: list, filtering, selection rules, messages and Invite to project.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project with at least 3 members: User A (owner), User B, User C.
- Chat C1 owned by User A, shared with User B.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Share > Team and focus the search | A dropdown floats over the window (not clipped): first row "Whole team: <n> teammates", then members not yet in the list, by name |
| 2 | Type a part of a name (start, then middle) | The list is filtered by any part of the name |
| 3 | Click a person, then click Whole team | Click toggles a row (highlight and check). Picking Whole team clears single people and vice versa. Footer "<n> selected"; Add is disabled at 0 |
| 4 | Type the name of User B, then a name that does not exist | "<User B> already has access" / "No matches found". Under each: "Not in the project? Invite to project" |
| 5 | Add Whole team, Save, and focus the search again | "Everyone already has access" |
| 6 | Click "Invite to project" | The same "Invite users" window as Settings > Users opens (emails separated by commas, project roles). Cancel closes it |
| 7 | Pick a person and press Escape; repeat with a click outside | The dropdown closes; the picked person is not added |

---

## Expected Final State

The picker lists only valid candidates and follows the selection rules.
