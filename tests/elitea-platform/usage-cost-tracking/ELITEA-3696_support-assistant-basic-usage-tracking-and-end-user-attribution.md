---
id: ELITEA-3696
title: "Support Assistant records input/output tokens per query, attributed to the real end-user, visible in Analytics within ~5 min"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, support-assistant]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6574"]
---

# ELITEA-3696: Support Assistant records input/output tokens per query, attributed to the real end-user, visible in Analytics within ~5 min

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify each user query to the Support Assistant records input tokens (query + context) and output tokens (AI response), that the total appears in Analytics within ~5 minutes, and that the spend is attributable to the real end-user — not merged into "system" usage — consistent with the auto-enrollment-as-viewer design (first-time user is auto-enrolled as viewer in the hidden Support Assistant project on first call to `GET /v2/support_assistant/conversations`).

---

## Preconditions

- Logged in to {{base_url}} as a known test user who has **not** previously used Support Assistant (to observe first-time auto-enrollment), or any known test user if auto-enrollment is already in place.
- Support Assistant is enabled (not disabled by admin).

---

## Test Data

| Field | Value |
|-------|-------|
| Query | "How do I create a new agent?" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant launcher and send the test query. | Support Assistant responds. |
| 2 | Within 5 minutes, check Analytics/`usage_event` for a corresponding row. | A row is present with non-zero input tokens (query + context) and output tokens (AI response). |
| 3 | Inspect the row's user attribution. | Attributed to the real, known test end-user — not a generic "system" user. |
| 4 | Confirm the conversation does not appear in the user's regular conversation listing. | Consistent with Support Assistant being backed by a hidden project excluded from the normal project list. |

---

## Expected Final State

Support Assistant usage is recorded per query with correct input/output tokens, attributed to the real end-user, visible in Analytics within ~5 minutes.

---

## Pass/Fail Criteria

**Pass:**
- Row appears within 5 minutes with correct, non-zero input/output tokens.
- Attribution is to the real end-user, not merged into system usage.

**Fail:**
- No row appears within 5 minutes.
- Usage is attributed to a generic/system user instead of the real end-user.
