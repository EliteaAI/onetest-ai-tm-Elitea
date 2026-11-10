---
id: ELITEA-4616
title: "A full backup-then-restore round trip (after deleting the original chats) reproduces the exact chat and message count, order, and content — not just 'a chat exists afterward'"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, data-integrity, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4616: Full round trip: backup → delete → restore reproduces exact message count, order, and content

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 2 chats: Chat 1 — send 3 messages in sequence: **"First
  message"**, **"Second message"**, **"Third message"** (note the exact order and wording). Chat 2 — send 1
  message, then upload 1 file as the user (note the exact filename). Back up Project A with **"All chats with
  attachments"**.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Delete both Chat 1 and Chat 2 from Project A. | Project A now has zero chats. |
| 2 | Restore the backup into Project A, Preview only unchecked, Replace unchecked, selecting **"Restore all chats with attachments"**. | Result shows **"Chats: 2 restored, 0 skipped"**. |
| 3 | Open the restored version of Chat 1. Count its messages and read their content/order. | **Exactly 3 messages**, in the **exact original order** — "First message", "Second message", "Third message" — with no reordering, merging, or content corruption. |
| 4 | Open the restored version of Chat 2. | **1 message** present, plus the attachment — same filename as noted in Preconditions, and it opens/downloads correctly. |

### Expected Final State
A full round trip after real deletion of the originals reproduces exact message count, order, and content for both a plain-text chat and an attachment-bearing chat.

### Pass/Fail Criteria
**Pass:** Both chats restore with exact message count/order/content, attachment included and working.
**Fail:** Any message count/order/content mismatch, or a non-working/missing attachment.
