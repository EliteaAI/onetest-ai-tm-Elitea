---
id: ELITEA-4458
title: "Two attachments sharing the exact same filename export and import correctly as distinct entries"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, issue:6903, issue:6904, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904"]
---

# ELITEA-4458: Two attachments sharing the exact same filename export and import correctly as distinct entries

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that two attachments with the identical filename (one uploaded, one generated) both export and import correctly as distinct entries, with no overwrite or collision.

---

## Preconditions

- Ability to attach a user-uploaded file and separately trigger an AI/agent-generated file in the same chat.

## Test Data

| Field | Value |
|-------|-------|
| First message | "Read this file and add" |
| Shared filename | `AI-Native-Engineer.pdf` (one Uploaded, one Generated) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a chat. Send the first message "Read this file and add". Upload one file named `AI-Native-Engineer.pdf`. In a follow-up message, ask an agent/tool to generate a file and explicitly name the generated output `AI-Native-Engineer.pdf` as well (same literal filename as the uploaded one). | Chat now contains 2 attachments with the identical filename — one Uploaded, one Generated. |
| 2 | Export this chat "With attachments". Import the resulting file into any project. Check the attachment preview during import. | Preview shows both `AI-Native-Engineer.pdf` rows as distinct entries — correct individual sizes, one tagged Uploaded, one tagged Generated — with the combined total size correctly summed. No overwrite, no collision. |
| 3 | Complete the import and download both attachments from the resulting chat. | Both files download correctly and independently — not the same file duplicated, not one overwriting the other. |

## Expected Final State

Two identically-named attachments from different sources survive export/import as fully distinct entries.

## Pass/Fail Criteria

**Pass:**
- Both duplicate-named attachments show distinctly with correct sizes/types and combined total; both download correctly.

**Fail:**
- Either attachment missing, overwritten, or miscounted.
