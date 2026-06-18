---
id: ELITEA-1182
title: "Agent and Pipeline Toolkits panel shows all three credential indicators with warning message for invalid credentials; valid credentials show only \"Open in new tab\""
priority: critical
type: functional
module: credential-actions-and-status-indicators
status: ready
execution_type: automated
tags: [feat:credentials, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5114]
---
# ELITEA-1182: Agent and Pipeline Toolkits panel shows all three credential indicators with warning message for invalid credentials; valid credentials show only "Open in new tab"

**Module:** Credential Actions And Status Indicators · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Agent menu and Pipeline configuration Toolkits panel exposes "Open in new tab", "Reload", Warning/Error status indicator, and a clear warning text message for invalid credentials — each with a correct tooltip — while valid credentials show only the "Open in new tab" icon.

**Coverage:**
- "Open in new tab" icon present and with tooltip in Agent menu (invalid credential)
- "Reload" icon present and with tooltip in Agent menu (invalid credential)
- Warning/Error indicator present in Agent menu (invalid credential)
- Warning text message containing "Authentication failed:" displayed in Agent menu (invalid credential)
- Valid credentials in Agent menu show only "Open in new tab" — no Reload, no error indicator, no warning message
- Same four checks verified for Pipelines: "Open in new tab", "Reload", Warning/Error indicator, warning text message "Authentication failed:"
- Valid credentials in Pipeline show only "Open in new tab" — no Reload, no error indicator

## Preconditions

- User logged into {{base_url}}
- Agent A configured with a toolkit referencing an invalid credential
- Agent B (or same agent with another toolkit) configured with a toolkit referencing a valid credential
- Pipeline A configured with a toolkit referencing an invalid credential
- Pipeline B (or same pipeline with another toolkit) configured with a toolkit referencing a valid credential

## Test Data

| Field | Value |
|---|---|
| Agent A | agent configured with broken/invalid toolkit credential |
| Agent B | agent configured with correctly authenticated toolkit credential |
| Pipeline A | pipeline configured with broken/invalid toolkit credential |
| Pipeline B | pipeline configured with correctly authenticated toolkit credential |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A (with the invalid credential toolkit) from the Agents section. Navigate to the Agent menu / inline Toolkits panel. | Toolkits panel is visible with credential entries. |
| 2 | Observe the credential entry for the invalid credential. | "Open in new tab" icon is present. |
| 3 | Hover over the "Open in new tab" icon. | Tooltip appears. Text matches expected label (e.g., "Open in new tab"). Not blank. |
| 4 | Observe the same credential entry. | "Reload" icon is present. |
| 5 | Hover over the "Reload" icon. | Tooltip appears. Text matches expected label (e.g., "Reload and apply changes"). Not blank. |
| 6 | Observe the same credential entry. | Warning/Error status indicator is visible. |
| 7 | Observe the text warning message displayed near the credential entry. | Warning message is visible and contains "Authentication failed:" text (e.g., "Authentication failed: Invalid bearer token"). Message is user-friendly, not a raw technical error. |
| 8 | Open Agent B (with the valid credential toolkit). Navigate to the Agent menu / inline Toolkits panel. | Toolkits panel visible with valid credential entry. |
| 9 | Observe the credential entry for the valid credential. | "Open in new tab" icon is visible. |
| 10 | Confirm no Reload icon is shown for the valid credential. | Reload icon is absent for the valid credential entry. |
| 11 | Confirm no Warning/Error status indicator and no warning message is shown for the valid credential. | No error/warning badge and no warning text message displayed for the valid credential. |
| 12 | Open Pipeline A (configured with a toolkit referencing an invalid credential) from the Pipelines section. Navigate to the pipeline configuration and locate the Toolkits panel. | Toolkits panel is visible with credential entries. |
| 13 | Observe the credential entry for the invalid credential in Pipeline A. | "Open in new tab" icon is present. |
| 14 | Hover over the "Open in new tab" icon in Pipeline A. | Tooltip appears. Text matches expected label (e.g., "Open in new tab"). Not blank. |
| 15 | Observe the same credential entry in Pipeline A. | "Reload" icon is present. |
| 16 | Hover over the "Reload" icon in Pipeline A. | Tooltip appears. Text matches expected label (e.g., "Reload and apply changes"). Not blank. |
| 17 | Observe the same credential entry in Pipeline A. | Warning/Error status indicator is visible. |
| 18 | Observe the text warning message displayed near the credential entry in Pipeline A. | Warning message is visible and contains "Authentication failed:" text (e.g., "Authentication failed: Invalid bearer token"). Message is user-friendly, not a raw technical error. |
| 19 | Open Pipeline B (configured with a toolkit referencing a valid credential) from the Pipelines section. Navigate to the Toolkits panel. | Toolkits panel visible with valid credential entry. |
| 20 | Observe the credential entry for the valid credential in Pipeline B. | "Open in new tab" icon is visible. |
| 21 | Confirm no Reload icon is shown for the valid credential in Pipeline B. | Reload icon is absent for the valid credential entry. |
| 22 | Confirm no Warning/Error status indicator and no warning message is shown for the valid credential in Pipeline B. | No error/warning badge and no warning text message displayed for the valid credential. |

## Expected Final State

No error/warning badge and no warning text message displayed for the valid credential.

## Pass/Fail Criteria

**Pass:**
- All three icons/indicators present for invalid credentials in Agent menu
- Tooltips present with meaningful text for "Open in new tab" and "Reload"
- Warning text message containing "Authentication failed:" visible for invalid credentials in Agent menu
- Valid credentials in Agent menu show only "Open in new tab" — no Reload, no warning
- All three icons/indicators present for invalid credentials in Pipeline configuration
- Tooltips present with meaningful text for "Open in new tab" and "Reload" in Pipeline
- Warning text message containing "Authentication failed:" visible for invalid credentials in Pipeline
- Valid credentials in Pipeline show only "Open in new tab" — no Reload, no warning

**Fail:**
- Any icon/indicator missing for invalid credential in Agent menu or Pipeline
- Any tooltip blank, missing, or showing a raw key
- Warning message absent, does not contain "Authentication failed:", or shows a raw technical error string (e.g., raw JSON/Python traceback)
- Reload or Warning/Error indicator shown for a valid credential
- "Open in new tab" missing for a valid credential
