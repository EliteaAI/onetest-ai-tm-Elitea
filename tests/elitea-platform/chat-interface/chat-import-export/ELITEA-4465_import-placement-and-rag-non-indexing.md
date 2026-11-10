---
id: ELITEA-4465
title: "Import never lands inside an open/selected folder, and never auto-indexes attachments for RAG"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4465: Import never lands inside an open/selected folder, and never auto-indexes attachments for RAG

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a chat import always lands in the root "Today" group regardless of which folder is open/selected, and that imported attachments are never automatically indexed for RAG.

---

## Preconditions

- A folder already exists in the Chats list.
- A valid chat export containing a document-type attachment, in a project where attachment/RAG indexing is available.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Expand/select the existing folder in the Chats list. While it is open/selected, trigger Import and complete a valid import. | New chat has no folder assignment — appears in the root "Today" group, not inside the open folder. |
| 2 | Open the imported chat's document attachment, hover it. | Only standard actions shown (e.g. Download, Delete) — no indexing badge, spinner, or status of any kind. |

## Expected Final State

Import always lands outside any folder and never triggers automatic RAG indexing.

## Pass/Fail Criteria

**Pass:**
- Both steps match exactly.

**Fail:**
- Chat lands in the folder, or any auto-indexing observed.
