---
id: ELITEA-3684
title: "Build/Edit-with-AI model misconfiguration shows a clean error; no cost recorded if provider never received the request"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, edit-with-ai, error-handling]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3684: Build/Edit-with-AI model misconfiguration shows a clean error; no cost recorded if provider never received the request

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the model backing Build-with-AI or Edit-with-AI is misconfigured, a clean user-facing error is shown (no hang, no raw stack trace), no cost is recorded if the provider never received the request, and partial tokens are recorded (`is_error=true`) if the provider did receive the request before failing.

---

## Preconditions

- Logged in to {{base_url}} with edit permission on an agent.
- Ability to misconfigure the backing model/credential for Build/Edit-with-AI in the test environment (e.g. invalid credentials, consistent with the pattern confirmed for chat in ELITEA-2416).

---

## Test Data

| Field | Value |
|-------|-------|
| Misconfiguration | Invalid/expired credential on the model backing Build or Edit with AI |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Misconfigure the model/credential used by Build-with-AI or Edit-with-AI. | Misconfiguration is in place. |
| 2 | Invoke Build-with-AI (or Edit-with-AI) and observe the UI response. | A clean, user-facing error message is shown — no indefinite hang, no raw stack trace exposed. |
| 3 | Check Analytics/`usage_event` for a row from this call. | If the request never reached the provider (e.g. auth rejected before dispatch), no cost is recorded for this call. |
| 4 | If the test environment allows forcing a provider-side failure **after** the request is sent (e.g. a model that accepts the request then errors), repeat and check the resulting row. | A row is recorded with `is_error=true` and real (non-estimated) input token counts reflecting what was actually sent. |

---

## Expected Final State

A misconfigured model produces a clean UI error with no silent cost for never-dispatched requests, and real partial-token rows for requests that reached the provider before failing.

---

## Pass/Fail Criteria

**Pass:**
- UI shows a clean error, no stack trace, no indefinite hang.
- No-dispatch failures produce no cost; dispatched-then-failed calls produce `is_error=true` rows with real tokens.

**Fail:**
- Raw error/stack trace is shown to the user, or the UI hangs.
- A never-dispatched call is billed, or a dispatched-then-failed call produces no row at all.
