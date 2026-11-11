---
id: ELITEA-4642
title: "Chats deletion does not delete chat attachments or Artifacts-feature data"
priority: critical
type: integration
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- A project with: (a) a chat containing at least one file attachment, and (b) an unrelated file stored via the Artifacts feature, not attached to any chat

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat with attachment | QA-Chat-1 (one file attached) |
| Unrelated Artifacts file | QA-Artifact-1 (not linked to any chat) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Before deletion, confirm the chat's attachment and the unrelated Artifacts-feature file are both present and accessible | Both accessible |
| 2 | In Delete Project Data, select Chats only, complete the typed-DELETE confirmation flow | Deletion completes |
| 3 | Confirm the chat, its messages, participants, and share links are removed | Chat and chat-owned data no longer accessible |
| 4 | Check whether the attachment file from step 1 still exists and is retrievable | Attachment file is NOT deleted — still exists and retrievable |
| 5 | Check the unrelated Artifacts-feature file | Still present, unmodified, and accessible |

## Expected Final State

The chat and its messages/participants/share links are gone, but the attachment file and all Artifacts-feature data remain fully intact.

## Pass/Fail Criteria

**Pass:**
- Attachment and unrelated Artifacts data both survive the Chats deletion

**Fail:**
- The attachment is deleted (report as a defect — contrary to dev-confirmed expectation)
- Any Artifacts-feature data is affected
