---
id: ELITEA-4654
title: "Delete Project Data renders correctly below Back Up & Restore with no layout regression"
priority: medium
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

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General | Sections appear in order: Schedules, Back Up & Restore, Delete Project Data |
| 2 | Check the Back Up & Restore section's "Create a Backup" and "Restore from the Backup" buttons | Both remain fully visible and functional |
| 3 | Resize the browser window to a smaller viewport | Delete Project Data checkbox grid and buttons remain usable without overlapping or clipping |

## Expected Final State

No layout regression is introduced to Back Up & Restore or the overall page by the new section.

## Pass/Fail Criteria

**Pass:**
- All sections render correctly and remain functional at various viewport sizes

**Fail:**
- Any overlap, clipping, or broken functionality in Back Up & Restore or Delete Project Data layout
