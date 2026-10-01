---
id: ELITEA-3450
title: "Build/Edit-with-AI cost calculation uses cost_micro_usd precision; unpriced model is flagged, not silently $0"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, edit-with-ai, cost-calculation]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3450: Build/Edit-with-AI cost calculation uses cost_micro_usd precision; unpriced model is flagged, not silently $0

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify cost for a Build-with-AI or Edit-with-AI invocation is computed from `cost_micro_usd` (1e-6 USD precision) and reflected correctly in Analytics → Costs, and that a model with no price-catalog entry is explicitly flagged (`cost_source='unpriced'`) rather than silently shown as $0.

---

## Preconditions

- Logged in to {{base_url}} with edit permission on an agent.
- Access to at least one model known to be in the price catalog, and (if available in the test environment) one model known **not** to be in the price catalog.

---

## Test Data

| Field | Value |
|-------|-------|
| Priced model | Any model with a confirmed price-catalog entry |
| Unpriced model (if available) | Any model configured but without a price-catalog entry |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke Build-with-AI or Edit-with-AI using the priced model. | Call completes successfully. |
| 2 | Navigate to Analytics → Costs tab. | The corresponding row shows a correct, non-zero USD amount matching token counts × the model's known price. |
| 3 | Inspect the underlying `usage_event`/`cost_micro_usd` value if accessible (API or DB). | Cost is stored as an integer at 1e-6 USD precision, not a floating-point display rounding artifact. |
| 4 | If an unpriced model is available, invoke Build-with-AI or Edit-with-AI using it. | Call completes successfully. |
| 5 | Inspect the resulting row's cost fields. | Row shows `cost_source='unpriced'` with cost explicitly flagged as unknown — **not** a silent `$0`. |

---

## Expected Final State

Priced-model calls show correct USD cost in the Costs tab derived from `cost_micro_usd`; unpriced-model calls are explicitly flagged as unpriced, never silently $0.

---

## Pass/Fail Criteria

**Pass:**
- Costs tab shows correct, non-zero USD for the priced-model call.
- Unpriced-model call shows `cost_source='unpriced'`, not a bare $0.

**Fail:**
- Priced-model cost is $0, missing, or inconsistent with token counts × price.
- Unpriced-model call silently shows $0 with no `cost_source='unpriced'` flag — file as a bug (named #6571 acceptance criterion).
