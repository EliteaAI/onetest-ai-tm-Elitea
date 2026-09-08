---
id: ELITEA-3347
title: "Pipeline with OAuth Toolkit Executes Successfully via Chat Messages Trigger"
priority: critical
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit, execution]
requirements: [EliteaAI/elitea_issues#6128]
---

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- OAuth-requiring toolkit available and configured with valid credentials
- User has OAuth authentication set up for the toolkit

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| OAuth Toolkit | Azure SharePoint Delegated |
| Test Message | "List files in SharePoint site" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new pipeline with OAuth-requiring toolkit (Azure SharePoint Delegated) | Pipeline created with OAuth toolkit |
| 2 | Configure OAuth toolkit with valid credentials and permissions | OAuth toolkit configured successfully |
| 3 | Configure Entrypoint node with Chat Message trigger (auto-selected) | Chat Message trigger selected |
| 4 | Add action nodes using OAuth toolkit operations (e.g., list SharePoint files) | Pipeline canvas configured with OAuth toolkit actions |
| 5 | Save pipeline | Pipeline saved successfully |
| 6 | Navigate to chat interface and open pipeline | Pipeline available in chat |
| 7 | Send message to trigger pipeline: "List files in SharePoint site" | Message sent successfully |
| 8 | Verify pipeline execution starts | Pipeline execution begins |
| 9 | Verify OAuth toolkit actions execute without authentication errors | OAuth operations complete successfully |
| 10 | Verify pipeline completes and returns results | Pipeline completes with success status |
| 11 | Check execution history | Execution appears with Chat Message trigger notification |
| 12 | Add second OAuth toolkit (e.g., Google Drive OAuth) to same pipeline | Second OAuth toolkit added |
| 13 | Trigger pipeline via chat again | Pipeline executes successfully |
| 14 | Verify both OAuth toolkit actions execute correctly | Both OAuth operations complete without errors |

## Expected Final State

Pipeline with OAuth toolkit(s) executes successfully via Chat Messages trigger. OAuth authentication works correctly. Multiple OAuth toolkits can be used in same pipeline.

## Pass/Fail Criteria

**Pass:**
- Pipeline executes via Chat Messages trigger
- OAuth toolkit actions execute without authentication errors
- Pipeline completes successfully and returns results
- Execution logged in run history with Chat Message trigger
- Multiple OAuth toolkits work in same pipeline

**Fail:**
- Pipeline fails to execute via Chat Messages
- OAuth authentication errors occur
- Pipeline execution fails or hangs
- No execution history logged
- Multiple OAuth toolkits cause conflicts
