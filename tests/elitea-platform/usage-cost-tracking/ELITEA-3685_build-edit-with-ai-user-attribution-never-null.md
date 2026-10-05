---
id: ELITEA-3685
title: "Build/Edit-with-AI usage_event.user_id always resolves to the real invoking user, never NULL"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, edit-with-ai, attribution]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6568"]
---

# ELITEA-3685: Build/Edit-with-AI usage_event.user_id always resolves to the real invoking user, never NULL

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the `usage_event` row produced by a Build-with-AI or Edit-with-AI invocation always records the correct, real invoking `user_id` — by design, `user_id` is NOT NULL for every dispatch path (per #6568).

---

## Preconditions

- Logged in to {{base_url}} as a known, identifiable test user with edit permission on an agent.

---

## Test Data

| Field | Value |
|-------|-------|
| Test user | Known test account with a known user ID |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the known test user. | Session established for a specific, identifiable user. |
| 2 | Invoke Build-with-AI on a new agent. | Call completes successfully. |
| 3 | Inspect the resulting `usage_event` row's `user_id` field. | `user_id` equals the known test user's ID — not NULL, not a system/service placeholder. |
| 4 | Invoke Edit-with-AI on an existing agent as the same user. | Call completes successfully. |
| 5 | Inspect the resulting row's `user_id`. | Again equals the known test user's ID. |

---

## Expected Final State

Every Build/Edit-with-AI `usage_event` row carries the correct, non-NULL invoking user's ID.

---

## Pass/Fail Criteria

**Pass:**
- Both rows show the correct, non-NULL `user_id` matching the invoking test user.

**Fail:**
- Any row has a NULL, missing, or incorrect `user_id`.
