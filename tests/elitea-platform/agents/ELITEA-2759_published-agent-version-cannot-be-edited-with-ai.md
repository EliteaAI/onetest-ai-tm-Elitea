---
id: ELITEA-2759
title: "Agent with published version cannot be edited via Edit with AI"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- An Agent has a **published** version currently selected
- User is logged in with Editor or Admin role

## Test Data

| Field | Value |
|-------|-------|
| Agent version state | Published |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an Agent that has a published version selected | The published version's configuration page loads |
| 2 | Inspect the "Edit with AI" CTA | The CTA is either not visible, or disabled with an appropriate tooltip explaining published versions are not editable |
| 3 | If the CTA is clickable, click it and attempt to generate and apply a draft | An appropriate error message is shown indicating published versions cannot be edited via Edit with AI, and no change is applied |
| 4 | Refresh the page after step 3 (if attempted) | The Agent's published configuration remains unchanged |

## Expected Final State

The published Agent version's configuration is unmodified; the user is clearly informed that Edit with AI is unavailable for published versions.

## Pass/Fail Criteria

**Pass:**
- The CTA is absent/disabled for published versions, or any attempt to apply changes is blocked with a clear error and no data is modified

**Fail:**
- The CTA is fully usable on a published version and changes are silently applied, or apply fails without any error message shown to the user
