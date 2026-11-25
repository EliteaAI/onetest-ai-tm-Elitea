---
id: ELITEA-4650
title: "Progress indicator is shown while deletion is running"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Project with a large number of items (dozens+) in at least one selected type

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select a type with a large item count and submit the deletion via the confirmation modal | Deletion begins |
| 2 | Observe the UI while the operation is running | A progress indicator (spinner/progress bar/disabled-loading button or equivalent) is shown |
| 3 | Wait for completion | Progress indicator clears and is replaced by the completion result |

## Expected Final State

Progress feedback is visible throughout the operation and clears appropriately upon completion.

## Pass/Fail Criteria

**Pass:**
- Progress indicator shown throughout and clears on completion

**Fail:**
- No progress feedback, or it does not clear/transition correctly
