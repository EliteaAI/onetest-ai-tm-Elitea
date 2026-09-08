---
id: ELITEA-3346
title: "Webhook URL Becomes Invalid After OAuth Toolkit Added to Pipeline"
priority: high
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit, webhook, execution]
requirements: [EliteaAI/elitea_issues#6128]
---

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- Non-OAuth toolkit available for initial setup
- OAuth-requiring toolkit available (e.g., Google Drive OAuth MCP)
- User has ability to send HTTP POST requests (curl, Postman, or similar tool)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| OAuth Toolkit | Google Drive OAuth MCP |
| Non-OAuth Toolkit | JIRA Toolkit |
| Webhook Type | Custom |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create pipeline with non-OAuth toolkit (JIRA) | Pipeline created successfully |
| 2 | Configure Entrypoint node with Webhook trigger (Custom type) | Webhook trigger configured, URL and secret generated |
| 3 | Copy webhook URL and secret value | Webhook URL and secret copied successfully |
| 4 | Save pipeline | Pipeline saved with Webhook trigger |
| 5 | Send POST request to webhook URL with correct authentication | Pipeline executes successfully |
| 6 | Verify execution appears in run history with Webhook trigger notification | Webhook execution logged in run history |
| 7 | Edit pipeline and add OAuth-requiring toolkit (Google Drive OAuth MCP) | OAuth toolkit added successfully |
| 8 | Save pipeline (Chat Message should be auto-selected) | Pipeline saved with Chat Message trigger |
| 9 | Send POST request to the same webhook URL with same authentication | Pipeline does NOT execute |
| 10 | Verify appropriate error response (e.g., 404 Not Found or "Webhook trigger disabled") | Error response received indicating webhook is disabled |
| 11 | Check execution history | No new webhook executions after OAuth toolkit was added |
| 12 | Manually trigger pipeline via chat interface | Pipeline executes successfully via Chat Message trigger |

## Expected Final State

Webhook URL no longer triggers pipeline execution. Pipeline executes successfully via Chat Message trigger. Previous webhook execution history remains visible.

## Pass/Fail Criteria

**Pass:**
- Webhook URL stops working after OAuth toolkit added
- Appropriate error response returned on webhook POST request
- No new webhook executions in run history
- Pipeline executes successfully via Chat Message trigger
- Previous webhook execution history remains visible

**Fail:**
- Webhook continues working with OAuth toolkit present
- No error response on webhook request
- OAuth authentication errors appear in logs
- Pipeline fails to execute via Chat Message trigger
- Previous execution history is lost
