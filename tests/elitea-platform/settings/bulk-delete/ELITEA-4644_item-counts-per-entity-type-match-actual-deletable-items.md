---
id: ELITEA-4644
title: "Item counts per entity type match actual deletable items (project-owned, not just own)"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Team project with items of multiple types created by at least two different users

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity type under test | Pipelines |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin, independently count each entity type via its native list view, including items created by other users | Independent counts recorded |
| 2 | Open Delete Project Data and compare displayed counts against the independently determined counts | Displayed counts match for every type |
| 3 | Select Pipelines and complete the deletion | Deletion completes |
| 4 | Check the Pipelines list afterward | Number of items actually removed matches the count displayed before deletion |

## Expected Final State

Displayed counts are accurate and match exactly what gets deleted.

## Pass/Fail Criteria

**Pass:**
- Displayed count == independently verified count == actual deleted count

**Fail:**
- Any mismatch between displayed, verified, or actual deleted counts
