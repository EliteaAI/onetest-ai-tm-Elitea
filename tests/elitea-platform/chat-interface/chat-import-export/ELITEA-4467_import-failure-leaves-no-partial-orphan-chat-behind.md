---
id: ELITEA-4467
title: "A forced mid-import failure (network loss) leaves zero residual state, no partial or orphan chat"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4467: A forced mid-import failure (network loss) leaves zero residual state, no partial or orphan chat

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a chat import either fully succeeds or leaves zero residual state — never a partial/orphan chat — when the connection is lost mid-import.

---

## Preconditions

- A valid chat export file.
- A way to briefly disable the network connection.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start an import, briefly disable the network mid-upload/commit. | Import fails with a toast such as "Import failed: <reason>. Nothing was imported." |
| 2 | Refresh the chat list. | No partial/orphan chat appears. |

## Expected Final State

A failed import either fully succeeds or leaves zero residual state — never a partial/orphan chat.

## Pass/Fail Criteria

**Pass:**
- Both steps match exactly.

**Fail:**
- An orphaned/partial chat appears after a forced failure.
