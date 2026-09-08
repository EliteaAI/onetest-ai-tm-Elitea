---
id: ELITEA-3345
title: "Scheduled Execution Stops After OAuth Toolkit Added to Pipeline"
priority: high
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit, execution]
requirements: [EliteaAI/elitea_issues#6128]
---

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- Non-OAuth toolkit available for initial setup
- OAuth-requiring toolkit available (e.g., Azure SharePoint Delegated)
- User can wait 5-10 minutes to verify scheduled execution behavior

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Schedule Cron | */5 * * * * (every 5 minutes for testing) |
| OAuth Toolkit | Azure SharePoint Delegated |
| Non-OAuth Toolkit | GitHub Toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create pipeline with non-OAuth toolkit (GitHub) | Pipeline created successfully |
| 2 | Configure Entrypoint node with Schedule trigger (*/5 * * * *) | Schedule trigger configured to run every 5 minutes |
| 3 | Save and activate pipeline | Pipeline saved in active state |
| 4 | Wait 5 minutes and check execution history | Pipeline executes automatically on schedule |
| 5 | Verify scheduled execution in run history | Execution appears with Schedule trigger notification |
| 6 | Edit pipeline and add OAuth-requiring toolkit (Azure SharePoint Delegated) | OAuth toolkit added successfully |
| 7 | Save pipeline (Chat Message should be auto-selected) | Pipeline saved with Chat Message trigger |
| 8 | Wait for next scheduled execution time (5+ minutes) | Pipeline does NOT execute on schedule |
| 9 | Check execution history after waiting period | No new scheduled executions after OAuth toolkit was added |
| 10 | Verify no OAuth authentication errors in logs | No authentication errors logged (scheduled trigger simply doesn't fire) |
| 11 | Manually trigger pipeline via chat interface | Pipeline executes successfully via Chat Message trigger |

## Expected Final State

Pipeline executes successfully via Chat Message trigger but does not execute on schedule. No scheduled executions occur after OAuth toolkit was added.

## Pass/Fail Criteria

**Pass:**
- Scheduled executions stop after OAuth toolkit added
- No new scheduled executions appear in run history
- No OAuth authentication errors in logs
- Pipeline executes successfully via Chat Message trigger
- Previous scheduled execution history remains visible

**Fail:**
- Pipeline continues executing on schedule with OAuth toolkit
- OAuth authentication errors appear in logs
- Pipeline fails to execute via Chat Message trigger
- Previous execution history is lost
