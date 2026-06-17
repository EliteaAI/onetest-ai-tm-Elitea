---
id: ELITEA-1218
title: "SharePoint Toolkit — Site Path Case Sensitivity Handling"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1218: SharePoint Toolkit — Site Path Case Sensitivity Handling

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Site Path value with uppercase letters is handled consistently — either silently normalized or rejected with a clear validation message — with no silent failures or HTTP 500 errors. Trailing slashes are accepted by the system and do not hinder tool execution; the UI does not trim them explicitly.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit using a tenant-only credential
- /teams/TestTeam site accessible

## Test Data

Variation 1: Teams/TestTeam (uppercase T)
Variation 2: teams/TestTeam/ (trailing slash) — accepted as-is; tool execution expected to succeed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the SharePoint toolkit. Set Site Path to Teams/TestTeam (uppercase T). Click Save. | Save completes. Either the value is normalized to teams/TestTeam silently, or a clear validation message is shown. |
| 2 | In Test Settings, select Get files list, click Run Tool. | Either files from /teams/TestTeam are returned (normalization), or a clear user-facing error is shown. No HTTP 500 or stack trace. |
| 3 | Set Site Path to teams/TestTeam/ (trailing slash). Click Save. | Save completes. The trailing slash is preserved as entered — the UI does not trim it. No validation error is shown. |
| 4 | In Test Settings, select Get files list, click Run Tool. | Files from /teams/TestTeam are returned successfully. The trailing slash does not cause an error or prevent tool execution. |

## Expected Final State

Files from /teams/TestTeam are returned successfully. The trailing slash does not cause an error or prevent tool execution.

## Pass/Fail Criteria

Pass:
- Uppercase variation results in either successful normalization (tool returns data) or a clear user-facing validation message; no HTTP 500
- Trailing slash variation saves without error, the value is preserved as-is in the field, and Get files list executes successfully

Fail:
- Uppercase variation silently fails (no data, no error message) or returns HTTP 500
- Trailing slash variation causes a tool error, HTTP 500, or prevents data retrieval
