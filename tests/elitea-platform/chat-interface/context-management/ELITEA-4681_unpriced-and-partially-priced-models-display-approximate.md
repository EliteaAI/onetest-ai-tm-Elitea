---
id: ELITEA-4681
title: "Unpriced and Partially Priced Models Display Approximate Cost Placeholders Correctly"
priority: high
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one unpriced model (e.g., custom/BYO-provider model not in the costs catalog) and one priced model are available as chat participants

## Test Data

| Field | Value |
|-------|-------|
| Priced model | Any platform-managed model present in the costs catalog |
| Unpriced model | A custom/BYO-provider model with no catalog price |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat, send a message using the priced model. | Usage totals show a concrete Approx. cost figure. |
| 2 | In the same chat, send a message using the unpriced model. | Approx. cost now displays as "≈ $X+" (not a plain dollar figure, and never exactly "$0.00"). |
| 3 | Hover/click the cost info icon. | Tooltip explains that some models used in this chat have no catalog price. |
| 4 | Start a new chat using ONLY the unpriced model and send a message. | Approx. cost displays as "—" (dash), not "$0.00" and not an error. |
| 5 | Inspect Input/Output token counts in both scenarios. | Token counts are still tracked and displayed correctly even when cost cannot be fully determined. |

## Expected Final State

Cost display correctly distinguishes between fully priced, partially priced ("≈ $X+"), and fully unpriced ("—") scenarios, and never silently shows $0.00 due to a missing price.

## Pass/Fail Criteria

**Pass:**
- Mixed priced/unpriced chat shows "≈ $X+" with the correct tooltip
- Fully unpriced chat shows "—"
- Token counts remain accurate regardless of pricing status

**Fail:**
- Cost shows as "$0.00" when a model is actually unpriced
- The "≈ $X+" or "—" states are not shown as documented
- Token counts are missing or incorrect when cost cannot be determined
