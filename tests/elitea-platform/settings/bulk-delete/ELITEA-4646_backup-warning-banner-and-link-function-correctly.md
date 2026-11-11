---
id: ELITEA-4646
title: "Backup warning banner and Back Up & Restore link function correctly"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Expected banner text | "We strongly recommend creating and verifying a backup before deleting project data. This action cannot be undone." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Delete Project Data | Warning banner visible with the expected text |
| 2 | Click the "Go to Back Up & Restore" link | Page scrolls to or navigates to the Back Up & Restore section |
| 3 | Select/deselect various entity-type checkboxes and re-check banner visibility | Banner remains visible regardless of checkbox selection state |

## Expected Final State

The warning banner and its link are present and functional at all times, independent of checkbox state.

## Pass/Fail Criteria

**Pass:**
- Banner text correct, link navigates correctly, always visible

**Fail:**
- Banner text incorrect/missing, link broken, or banner disappears based on selection
