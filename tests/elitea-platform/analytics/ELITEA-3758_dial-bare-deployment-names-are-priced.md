---
id: ELITEA-3758
title: "DIAL calls are priced even when the catalog lists the price under a provider-prefixed name"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, costs, dial, pricing, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6996", "EliteaAI/elitea_issues#6355"]
---

# ELITEA-3758: DIAL calls are priced even when the catalog lists the price under a provider-prefixed name

**Module:** analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a DIAL model whose price exists only under a provider-prefixed catalog name (e.g. `azure/<name>`, `vertex_ai/<name>`) gets the correct cost.

---

## Preconditions

- Admin access to Admin → Model Prices.
- A DIAL model configuration whose Model Name has no exact catalog row, but whose provider-prefixed name does.

---

## Test Data

| Field | Value |
|-------|-------|
| Model | A DIAL deployment found in Model Prices only with a provider prefix |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Model Prices, search the model name. | Only the prefixed row exists; note its input, output and cache rates. |
| 2 | Run an agent once on the DIAL model. | It answers. |
| 3 | Read the call from `analytics_run_detail` (tokens and `cost_nano_usd`). | Cost is non-zero. |
| 4 | Compute tokens × catalog rates (input, output, cache read, cache write). | Equal to the recorded cost. |
| 5 | If the same bare name maps to several prefixed rows with different prices, run once more. | The call is left unpriced (and a warning is logged); it is not priced arbitrarily. |
| 6 | Check Analytics → Costs for the model. | The model shows the cost, not $0. |

---

## Expected Final State

DIAL usage is priced from the catalog regardless of prefix, and only when unambiguous.

---

## Pass/Fail Criteria

**Pass:**
- Cost equals tokens × catalog rates; ambiguous names stay unpriced.

**Fail:**
- Cost is 0 for a model that has a prefixed catalog price, or an ambiguous name is priced.
