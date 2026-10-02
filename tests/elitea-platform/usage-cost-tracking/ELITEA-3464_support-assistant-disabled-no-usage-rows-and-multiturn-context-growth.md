---
id: ELITEA-3464
title: "Support Assistant disabled by admin produces no usage rows (not just a hidden UI); multi-turn cost grows with context size"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, support-assistant]
requirements: ["EliteaAI/elitea_issues#6566"]
---

# ELITEA-3464: Support Assistant disabled by admin produces no usage rows (not just a hidden UI); multi-turn cost grows with context size

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when Support Assistant is disabled by an admin, **no usage rows are generated** while disabled — not merely that the launcher/panel UI is hidden. As a smoke check (not a deep-dive, since this duplicates ordinary chat multi-turn behavior already covered elsewhere), verify a multi-turn Support Assistant conversation's token/cost grows with accumulating context.

---

## Preconditions

- Admin access to toggle the Support Assistant feature flag.
- A known test end-user account for the multi-turn smoke check.

---

## Test Data

| Field | Value |
|-------|-------|
| Multi-turn queries | 3 sequential follow-up questions in one Support Assistant conversation |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As admin, disable Support Assistant. | Launcher and panel are absent for end-users (confirmed existing behavior). |
| 2 | Attempt to invoke Support Assistant via any route still available while disabled (if any API/UI path remains reachable). | No AI response is generated / feature is unavailable. |
| 3 | Check Analytics/`usage_event` for any new Support Assistant rows created during the disabled window. | **No** usage rows are generated while disabled. |
| 4 | Re-enable Support Assistant. | Launcher/panel reappear. |
| 5 | As the test end-user, send 3 sequential follow-up queries in one conversation. | Each turn gets a response. |
| 6 | Inspect the input token counts across the 3 turns. | Input tokens grow turn-over-turn as context accumulates, consistent with how the provider bills growing context. |

---

## Expected Final State

Disabling Support Assistant produces zero usage rows for the disabled window; multi-turn conversations show input tokens growing with accumulated context.

---

## Pass/Fail Criteria

**Pass:**
- No usage rows during the disabled window.
- Input tokens increase across turns in the multi-turn smoke check.

**Fail:**
- Any usage row is generated while Support Assistant is disabled.
- Input tokens do not grow with context across turns (unexpected flat/zero growth).
