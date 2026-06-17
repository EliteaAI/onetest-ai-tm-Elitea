---
id: ELITEA-1229
title: "[EliteaAI/elitea_issues#4660] SharePoint — Auto-Refresh End-to-End via Agent Chat and Pipeline Toolkit Node"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, feat:toolkits, integration, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1229: [EliteaAI/elitea_issues#4660] SharePoint — Auto-Refresh End-to-End via Agent Chat and Pipeline Toolkit Node

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** End-to-end verification of automatic token refresh in real integration contexts: (1) Agent Chat where the access token expires mid-session and a SharePoint tool call is made; (2) Pipeline with a SharePoint Toolkit node where the token is expired at run time. In both cases, the system must refresh silently and complete the operation without user login interaction.

## Preconditions

SharePoint toolkit authenticated with valid refresh token
Access token is expired (past expires_at)
For Agent Chat: agent configured with SharePoint toolkit and at least one tool enabled
For Pipeline: pipeline with a Toolkit Node using SharePoint configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With an expired access token (and valid refresh token), open an agent chat session using a SharePoint-enabled agent. Send a message requesting a SharePoint operation (e.g., 'list files in the Documents folder'). | SharePoint tool call fires. Token refresh happens automatically in the background. The tool result (file list) is returned in the chat. No Logon button or re-authentication prompt appears. |
| 2 | With an expired access token (and valid refresh token), run a Pipeline that includes a SharePoint Toolkit Node (configured to perform a read or write operation). | Pipeline run completes successfully. The SharePoint Toolkit Node result is visible in the run output. No token-expired error. No manual login prompt. |

## Expected Final State

Pipeline run completes successfully. The SharePoint Toolkit Node result is visible in the run output. No token-expired error. No manual login prompt.

## Pass/Fail Criteria

Agent Chat: SharePoint tool result returned in chat with no Logon prompt when token expired but refresh token valid
Pipeline: Pipeline run completes successfully when token expired but refresh token valid
No 'tool execution failed' error in either context
No Logon modal interrupts the Pipeline run
