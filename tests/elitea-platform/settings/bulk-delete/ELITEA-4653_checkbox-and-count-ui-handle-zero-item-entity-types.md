---
id: ELITEA-4653
title: "Checkbox and count UI handle zero-item entity types correctly"
priority: medium
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- A project where at least one entity type (e.g., MCPs) currently has zero items

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Zero-item entity type | MCPs |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Delete Project Data | The zero-item type displays a count of 0 next to its label |
| 2 | Attempt to check the checkbox for that type | Checkbox can be checked (or is appropriately disabled per intended behavior) without a UI error |
| 3 | If checkable, check it along with other non-zero types and submit the deletion | Operation completes without error, reporting 0 deleted items for the zero-item type |

## Expected Final State

The zero-item type is handled gracefully in both display and deletion flow, without UI errors.

## Pass/Fail Criteria

**Pass:**
- No UI error; 0-item type reported accurately

**Fail:**
- UI error, broken layout, or incorrect reporting for the zero-item type
