---
id: ELITEA-4815
title: "Export availability follows a participant's role changes and is enforced server-side"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, chat-export, share-chat, feat:roles-permissions, issue:7723, p1]
requirements: [EliteaAI/elitea_issues#7723, EliteaAI/elitea_issues#7489]
---

# ELITEA-4815: Export availability follows a participant's role changes and is enforced server-side

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that Export for a chat participant who is not the owner follows that participant's current project role (hidden for Viewer, available for Editor), that a Viewer cannot export by calling the export request directly, and that every route into the chat hides Export for a Viewer.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project where User A is admin and owns chat C1 (with at least one message and one attachment) shared with User B (selected people).
- User B has the Editor role on the project.
- Browser DevTools (Network tab) available.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B (Editor), open C1 and its "⋮" menu. Click Export and start the export, with DevTools Network open | Export is shown; the export succeeds and the file downloads. Note the export request (URL, method, body) |
| 2 | As User A, change User B's role to Viewer in Settings > Users | Role saved |
| 3 | As User B, reload the page, open C1 and its "⋮" menu | Export is not shown; the Export chat window cannot be opened |
| 4 | As User B (Viewer), replay the export request noted in step 1 (DevTools "Copy as fetch" and run it in the Console) | The request is rejected with a permission error (e.g. 403); no file is produced |
| 5 | As User B (Viewer), open C1 through its copied chat link in a new tab, and through a mention notification in C1 (User A mentions User B) | C1 opens; in both cases Export is not shown in the "⋮" menu |
| 6 | As User A, change User B's role back to Editor; as User B reload and open the "⋮" menu of C1 | Export is shown again and the export succeeds |
| 7 | As User A (owner), open the "⋮" menu of C1 and export | Export is shown and the export succeeds throughout |

---

## Expected Final State

Export for a participant who is not the owner follows that participant's current role: Viewer gets no Export in the UI and is rejected by the server; Editor gets Export. The owner keeps Export.
