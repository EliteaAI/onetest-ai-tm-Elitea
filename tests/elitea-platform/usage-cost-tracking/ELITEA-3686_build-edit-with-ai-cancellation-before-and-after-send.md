---
id: ELITEA-3686
title: "Build/Edit-with-AI cancellation: no token record only if the backend call is actually aborted"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, edit-with-ai, cancellation]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3686: Build/Edit-with-AI cancellation: no token record only if the backend call is actually aborted

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that cancelling a Build-with-AI or Edit-with-AI invocation before the LLM call completes produces no token record **only when the backend call is actually aborted**. Closing the modal client-side does not guarantee the in-flight request was cancelled server-side, so both "cancel before send" and "close modal after send, before response" must be tested separately.

---

## Preconditions

- Logged in to {{base_url}} with edit permission on an agent.
- Ability to observe `usage_event` rows shortly after each attempt (Analytics or direct query).

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario A | Cancel before the request is sent (e.g. click Cancel immediately after opening the modal, before submitting) |
| Scenario B | Close the modal immediately after submitting, before the response returns |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Build-with-AI (or Edit-with-AI) modal and click Cancel/close **before** submitting any request (Scenario A). | No request was ever sent. |
| 2 | Check `usage_event`/Analytics for a corresponding row. | No row is produced — correct, since nothing was sent. |
| 3 | Open the modal again, submit a request, then **immediately close the modal** before the response returns (Scenario B). | Modal closes; underlying request may still be in flight server-side. |
| 4 | Wait a reasonable interval, then check `usage_event`/Analytics for a corresponding row. | If the backend call was actually cancelled server-side, no token row appears. If the backend call was **not** cancelled (ran to completion despite the closed modal), a row **does** appear with real tokens — record which behavior is observed. |

---

## Expected Final State

Scenario A produces no row (nothing was sent). Scenario B's outcome depends on whether the backend genuinely aborts the in-flight call — the actual observed behavior must be documented, not assumed.

---

## Pass/Fail Criteria

**Pass:**
- Scenario A: no row produced.
- Scenario B: the row/no-row outcome is consistent with whether the backend call was actually aborted (i.e. no "ghost" billing for a call the user believes was cancelled, if the product claims server-side cancellation).

**Fail:**
- Scenario A produces a row despite nothing being sent.
- Scenario B silently bills the user for a call they believed was cancelled, with no indication server-side cancellation failed.
