---
id: ELITEA-3344
title: "Chat Messages Trigger Automatically Selected When OAuth Toolkit Added"
priority: high
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit]
requirements: [EliteaAI/elitea_issues#6128]
---

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- OAuth-requiring toolkit available (e.g., Azure SharePoint Delegated)
- Non-OAuth toolkit available for initial configuration

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| OAuth Toolkit | Azure SharePoint Delegated |
| Non-OAuth Toolkit | GitHub Toolkit |
| Schedule Cron | 0 9 * * * (daily at 9 AM) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new pipeline with non-OAuth toolkit (GitHub) | Pipeline created with GitHub toolkit |
| 2 | Configure Entrypoint node with Schedule trigger (0 9 * * *) | Schedule trigger configured and saved |
| 3 | Save pipeline | Pipeline saves successfully with Schedule trigger |
| 4 | Edit pipeline and add OAuth-requiring toolkit (Azure SharePoint Delegated) | OAuth toolkit added to pipeline |
| 5 | Navigate to Entrypoint node Trigger configuration | Trigger has **automatically switched to Chat Message** |
| 6 | Verify Schedule trigger is disabled and deselected | Schedule trigger is grayed out and not selected |
| 7 | Save pipeline without manually selecting any trigger | Pipeline saves successfully |
| 8 | Close and reopen pipeline | Pipeline opens successfully |
| 9 | Check Entrypoint trigger configuration | Chat Message trigger is selected, Schedule remains disabled |
| 10 | Verify schedule configuration is cleared | No cron schedule visible in configuration |

## Expected Final State

Pipeline saved with Chat Message trigger automatically selected. Schedule trigger disabled and previous schedule configuration cleared.

## Pass/Fail Criteria

**Pass:**
- Chat Message automatically selected when OAuth toolkit added
- Schedule trigger disabled and deselected
- Pipeline saves successfully without manual trigger selection
- Schedule configuration cleared
- Trigger selection persists after save and reopen

**Fail:**
- User must manually select Chat Message trigger
- Schedule trigger remains selected
- Pipeline save fails or requires manual intervention
- Schedule configuration retained
