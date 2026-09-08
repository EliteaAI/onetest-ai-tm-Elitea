---
id: ELITEA-3343
title: "OAuth Toolkit Restricts Trigger Selection to Chat Messages Only"
priority: critical
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
- Non-OAuth toolkit available (e.g., GitHub Toolkit)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| OAuth Toolkit | Azure SharePoint Delegated |
| Non-OAuth Toolkit | GitHub Toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new pipeline and add Entrypoint node | Entrypoint node added successfully |
| 2 | Open Entrypoint node config and click Trigger dropdown | All three options visible: Chat Message, Schedule, Webhook (all enabled) |
| 3 | Add OAuth-requiring toolkit (Azure SharePoint Delegated) to pipeline | OAuth toolkit added successfully |
| 4 | Return to Entrypoint node and click Trigger dropdown | Chat Message is **enabled**, Schedule and Webhook are **disabled** (grayed out) |
| 5 | Hover over disabled Schedule trigger option | Explanatory tooltip appears: "Scheduled triggers are not supported with OAuth toolkits" or similar |
| 6 | Hover over disabled Webhook trigger option | Explanatory tooltip appears: "Webhook triggers are not supported with OAuth toolkits" or similar |
| 7 | Attempt to click disabled Schedule trigger | Button does not respond, remains disabled |
| 8 | Select Chat Message trigger and save pipeline | Pipeline saves successfully with Chat Message trigger |
| 9 | Remove OAuth toolkit from pipeline | OAuth toolkit removed successfully |
| 10 | Click Trigger dropdown again | All three triggers are now **enabled** again |

## Expected Final State

All three trigger options (Chat Message, Schedule, Webhook) are enabled when OAuth toolkit is removed from pipeline.

## Pass/Fail Criteria

**Pass:**
- Schedule and Webhook triggers disabled when OAuth toolkit present
- Chat Message trigger remains enabled
- Explanatory tooltips display on disabled triggers
- All triggers re-enabled when OAuth toolkit removed

**Fail:**
- Disabled triggers remain clickable
- No tooltips on disabled triggers
- Chat Message trigger also disabled
- Triggers remain disabled after OAuth toolkit removed
