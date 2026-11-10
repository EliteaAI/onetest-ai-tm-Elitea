---
id: ELITEA-4473
title: "Import modal shows exact specified text and a full round trip reproduces the exact message count/order/content"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, regression, e2e, issue:6904, p0]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4473: Import modal shows exact specified text and a full round trip reproduces the exact message count/order/content

**Module:** chat-interface · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm the Import modal's exact text, and that a full Import round trip reliably reproduces the exact message count, order, and content, including attachments.

---

## Preconditions

- Create a chat with at least 3 messages and at least 1 attachment. Note the exact message count. Export it "With attachments".

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Import, select the exported file. | Modal shows "Import chat" / hint text / "Choose file", then "checking file", then a preview showing the correct chat name, the correct message count (matching Preconditions), exported-at timestamp, and correct attachment row(s)/counter. |
| 2 | Import with all attachments selected. Count the resulting chat's messages and compare their order/content to the original. | New chat created at top of Today, auto-opened; every attachment downloadable correctly; message count matches exactly, and messages appear in the same order with the same content as the original. |
| 3 | Verify the original chat. | Unchanged. |

## Expected Final State

The full Import round trip works reliably with exact modal text and exact message-count/order/content preservation.

## Pass/Fail Criteria

**Pass:**
- Modal text matches exactly; message count/order/content match exactly; round trip completes correctly.

**Fail:**
- Any text mismatch, message count mismatch, wrong order, missing/corrupted attachment, or content mismatch after import.
