---
id: ELITEA-4466
title: "Imported chat always gets a brand-new id/uuid, never reusing the original, and messages display in correct chronological order"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, data-integrity, issue:6904, p0]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4466: Imported chat always gets a brand-new id/uuid, never reusing the original, and messages display in correct chronological order

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a newly imported conversation always receives a brand-new `id`/`uuid` distinct from the original, and that its messages display in correct chronological order matching the source chat.

---

## Preconditions

- A valid chat export file with at least 3 messages, in correct chronological order.
- Browser DevTools (Network tab) access.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Import the file. Inspect the commit response (Network tab). | New conversation has a brand-new `id`/`uuid`, distinct from the original. Original `uuid`/`project_id` are kept only as inert metadata, never reused as the live record's identity. `author_id` = the importer. |
| 2 | Open that imported chat in the UI. Count the messages and check their order against the original chat. | All messages present; displayed in correct chronological order (oldest first), matching the original — regardless of any ordering seen in the raw API response. |

## Expected Final State

Import always generates a fully new identity and always preserves message count/order.

## Pass/Fail Criteria

**Pass:**
- Both steps match exactly.

**Fail:**
- Any id/uuid reuse, or wrong message count/order.
