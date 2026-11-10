---
id: ELITEA-4577
title: "A chat containing Canvas-type content (e.g. AI-generated code) restores with the actual canvas content intact, not an empty or broken canvas"
priority: high
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4577: Canvas-type chat content survives backup and restore

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Functional

### Preconditions
- A project ("Project A") containing 1 chat: send a first message that causes the AI to generate code into a
  Canvas (e.g. ask it to "write a short Python function that reverses a string, opened in the canvas"). Note
  the exact canvas content shown. Back up Project A with **"All chats without attachments"**.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Delete this chat from Project A. | Project A now has zero chats. |
| 2 | Restore the Preconditions' backup into Project A, Preview only unchecked, Replace unchecked, selecting **"Restore all chats without attachments"**. | Result shows **"Chats: 1 restored, 0 skipped"**. |
| 3 | Open the restored chat and open its Canvas. | The canvas shows the **exact same code/content** noted in Preconditions — not an empty canvas, not a broken/placeholder render. |

### Expected Final State
Canvas content is a real part of what gets backed up and restored, with content fidelity confirmed.

### Pass/Fail Criteria
**Pass:** Canvas content after restore matches the original exactly.
**Fail:** Empty, broken, or incorrect canvas content after restore.
