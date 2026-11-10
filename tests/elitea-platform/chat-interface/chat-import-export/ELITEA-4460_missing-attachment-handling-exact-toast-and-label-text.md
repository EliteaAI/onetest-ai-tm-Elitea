---
id: ELITEA-4460
title: "Export's pre-export label, post-export toast, and Import's unavailable-attachment handling show exact text when a file is deleted from storage"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, bugfix, issue:6903, issue:6904, issue:7208, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7208"]
---

# ELITEA-4460: Export's pre-export label, post-export toast, and Import's unavailable-attachment handling show exact text when a file is deleted from storage

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Export's pre-export attachment-count label, its post-export warning toast, and Import's "unavailable" attachment handling all show the exact, correct text when an attachment has been deleted directly from storage (bug #7208 fix). This bug was originally intermittent before the fix (2 of 4 identical attempts failed — the warning simply didn't appear); repeat steps 1-4 at least 2-3 times with fresh files before concluding Pass.

---

## Preconditions

- Ability to have an agent/tool generate a file directly into the Artifacts bucket, and ability to delete a file directly from the Artifacts bucket (NOT via the chat message's own delete button — deleting via the message also removes the message's reference to it, a different, already-excluded scenario this test case does not cover).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a chat. Send a first message that has an agent/tool generate exactly 2 files into the Artifacts bucket as part of the response (so the chat has exactly 2 attachments, both still present in storage). | Chat created with 2 available attachments. |
| 2 | Delete one of the 2 generated files directly from the Artifacts bucket. | 1 of the 2 attachments is now missing from storage, but the chat message still references it. |
| 3 | Open Export modal on this chat, select "With attachments" — read the label before clicking Export. | Label reads the real, storage-verified breakdown, e.g. "With attachments (1 file · [size] · 1 unavailable)" — not a stale count that ignores the deletion. |
| 4 | Click Export. | Export completes; warning toast appears: "Chat exported. 1 file(s) could not be included." |
| 5 | Import the resulting file. Check the attachment preview. | The still-available file shows normally, selectable. The missing one shows disabled, labeled "Not available in archive", excluded from the selection count (e.g. "Selected 1 of 2 attachments ([size])"). |
| 6 | Complete the import. | The missing file's message shows as "<filename> (not imported)" in place, no download link; the available file imports and downloads correctly. |
| 7 | Create a second chat with exactly 1 generated attachment. Delete that single file directly from Artifacts. Open Export modal, select "With attachments" — read the label. | Label reads exactly: "With attachments (0 files · 1 unavailable)". Since there are 0 selectable files, the "With attachments" radio itself is disabled — cannot be selected at all. |

## Expected Final State

Both the pre-export label and the post-export toast always reflect the real, storage-verified state; Import always correctly flags and excludes whatever Export reported as unavailable.

## Pass/Fail Criteria

**Pass:**
- Every quoted label/toast/placeholder text matches exactly for both the 2-attachment and 1-attachment setups, across repeated attempts.

**Fail:**
- Any stale count, wrong/missing toast text, or incorrect Import-side label/placeholder on any attempt.
