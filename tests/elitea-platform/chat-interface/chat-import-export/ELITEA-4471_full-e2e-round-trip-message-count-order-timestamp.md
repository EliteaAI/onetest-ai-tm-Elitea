---
id: ELITEA-4471
title: "A full Export-then-Import round trip reproduces the exact message count, order, content, and timestamps, with and without attachments"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, e2e, issue:6903, issue:6904, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904"]
---

# ELITEA-4471: A full Export-then-Import round trip reproduces the exact message count, order, content, and timestamps, with and without attachments

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a full Export-then-Import round trip reproduces the exact message count, order, content, and timestamps, both for a no-attachment chat and an attachment-heavy chat, and that the original chat is provably untouched throughout.

---

## Preconditions

- Create Chat A: exactly 8 messages alternating user/AI (4 each), no attachments. Note the exact message count and the order of senders (user, AI, user, AI, ...).
- Create Chat B: a conversation resulting in at least 5 distinct attachments across multiple messages. Note the exact message count.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Export Chat A "Without attachments". Import the file. Open the imported chat and count its messages. | New chat created with the identical auto-derived name as Chat A. Message count matches Chat A's count exactly (8). Messages appear in the identical order (same alternating user/AI sequence) and with identical content. |
| 2 | Observe where the new chat lands. | New chat appears at the top of the "Today" group, auto-opens and is selected (URL changes to the new chat's id), even if Chat A isn't in Today. |
| 3 | Compare per-message timestamps between Chat A and the imported chat. | Timestamps match the original send times — not the import time. |
| 4 | Return to Chat A. | Completely unchanged — same id, same message count/content, same position. |
| 5 | Export Chat B "With attachments", all selected. Import it. Count the resulting chat's messages and attachments. | New chat created with the same message count as Chat B, same order; all attachments open/download correctly from the new chat's messages. |

## Expected Final State

Both round-trip variants reproduce the exact message count, order, content, and timestamps, landing correctly at the top of Today, with the original chat left untouched in every case.

## Pass/Fail Criteria

**Pass:**
- All 5 steps match exactly, including an exact message-count match in steps 1 and 5.

**Fail:**
- Any content/count/order/timestamp mismatch, incorrect placement, or any modification to the original chat.
