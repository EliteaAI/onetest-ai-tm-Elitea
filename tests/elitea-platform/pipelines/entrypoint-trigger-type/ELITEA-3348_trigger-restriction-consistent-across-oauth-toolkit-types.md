---
id: ELITEA-3348
title: "Trigger Restrictions Apply Consistently Across All OAuth Toolkit Types and MCPs"
priority: medium
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [pipeline, r-2.0.6, trigger, oauth, toolkit, mcp]
requirements: [EliteaAI/elitea_issues#6128]
---

## Preconditions

- User is logged in to `{{base_url}}` with pipeline edit permissions
- Multiple OAuth-requiring toolkits and MCPs available for testing

## Test Data

| OAuth Toolkit/MCP | Type | Expected Behavior |
|-------------------|------|-------------------|
| Azure SharePoint Delegated | Toolkit | Chat only |
| Google Drive OAuth | MCP | Chat only |
| Slack OAuth | MCP | Chat only |
| Microsoft Graph OAuth | MCP | Chat only |
| Salesforce OAuth | MCP | Chat only |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new pipeline and add Azure SharePoint Delegated toolkit | Pipeline created with OAuth toolkit |
| 2 | Open Entrypoint Trigger dropdown | Chat Message enabled, Schedule/Webhook disabled with tooltips |
| 3 | Verify tooltip text explains OAuth restriction clearly | Tooltip: "Scheduled/Webhook triggers are not supported with OAuth toolkits" |
| 4 | Select Chat Message trigger and save pipeline | Pipeline saves successfully |
| 5 | Trigger pipeline via chat | Pipeline executes successfully with OAuth authentication |
| 6 | Remove Azure SharePoint toolkit and add Google Drive OAuth MCP | Google Drive OAuth MCP added |
| 7 | Open Entrypoint Trigger dropdown | Chat Message enabled, Schedule/Webhook disabled with tooltips |
| 8 | Save and trigger pipeline via chat | Pipeline executes successfully |
| 9 | Replace with Slack OAuth MCP | Slack OAuth MCP added |
| 10 | Verify same trigger restrictions apply | Chat only, Schedule/Webhook disabled |
| 11 | Save and trigger pipeline via chat | Pipeline executes successfully |
| 12 | Replace with Microsoft Graph OAuth MCP | Microsoft Graph OAuth MCP added |
| 13 | Verify same trigger restrictions apply | Chat only, Schedule/Webhook disabled |
| 14 | Replace with Salesforce OAuth MCP | Salesforce OAuth MCP added |
| 15 | Verify same trigger restrictions apply | Chat only, Schedule/Webhook disabled |
| 16 | Save and trigger pipeline via chat | Pipeline executes successfully with Salesforce OAuth |

## Expected Final State

All OAuth-requiring toolkits and MCPs apply the same trigger restriction: Chat Message enabled, Schedule and Webhook disabled. All execute successfully via Chat Messages trigger.

## Pass/Fail Criteria

**Pass:**
- Trigger restrictions consistent across all OAuth toolkit types
- Chat Message trigger enabled for all OAuth toolkits/MCPs
- Schedule/Webhook disabled for all OAuth toolkits/MCPs
- Tooltips display consistently for all types
- All OAuth toolkits/MCPs execute successfully via chat

**Fail:**
- Inconsistent trigger restrictions across different OAuth types
- Some OAuth types allow Schedule/Webhook triggers
- Tooltips missing or inconsistent
- Authentication failures with certain OAuth types
