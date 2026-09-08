---
id: ELITEA-3343
title: "OAuth Toolkit Trigger Restriction — Chat Messages Only"
priority: critical
type: regression
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit, regression]
requirements: [EliteaAI/elitea_issues#6128]
---
# ELITEA-3343: OAuth Toolkit Trigger Restriction — Chat Messages Only

**Module:** Entrypoint Trigger Type · **Priority:** Critical · **Type:** Regression

**Objective:** Verifies that when a pipeline contains an OAuth-requiring toolkit (Azure SharePoint Delegated), the Entrypoint Trigger dropdown restricts available options to Chat Messages only, with Schedule and Webhook options disabled.

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- Azure SharePoint Delegated toolkit is available in the system
- Test pipeline can be created and edited

## Test Data

| Field | Value |
|-------|-------|
| Pipeline Name | OAuth Trigger Restriction Test |
| OAuth Toolkit | Azure SharePoint Delegated |
| Expected Enabled Trigger | Chat Messages |
| Expected Disabled Triggers | Schedule, Webhook |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new pipeline with default Entrypoint node | Pipeline created with Entrypoint node; Trigger defaults to Chat Messages |
| 2 | Open Entrypoint node config and click Trigger dropdown | All three trigger options visible: Chat Messages, Schedule, Webhook — all enabled |
| 3 | Close Entrypoint config; add Azure SharePoint Delegated toolkit to pipeline | OAuth toolkit successfully added to pipeline |
| 4 | Open Entrypoint node config again and click Trigger dropdown | Chat Messages is enabled (selectable); Schedule and Webhook are disabled (grayed out) |
| 5 | Verify Chat Messages trigger is still selected and functional | Chat Messages trigger remains selected; pipeline can be saved |
| 6 | Attempt to programmatically change trigger to Schedule via API or YAML | Change is rejected; trigger remains Chat Messages; error message indicates OAuth toolkit restriction |
| 7 | Remove OAuth toolkit from pipeline | OAuth toolkit successfully removed |
| 8 | Open Entrypoint Trigger dropdown again | All three trigger options are enabled again (Chat Messages, Schedule, Webhook) |

## Expected Final State

Pipeline with OAuth toolkit restricts triggers to Chat Messages only. After removing OAuth toolkit, all trigger types become available again.

## Pass/Fail Criteria

**Pass:**
- OAuth toolkit addition immediately restricts triggers to Chat Messages
- Schedule and Webhook options visually disabled (grayed out)
- Restriction cannot be bypassed via API or YAML
- Removing OAuth toolkit restores all trigger options

**Fail:**
- Schedule or Webhook can be selected with OAuth toolkit present
- Restriction can be bypassed programmatically
- Trigger options do not restore after OAuth toolkit removal
