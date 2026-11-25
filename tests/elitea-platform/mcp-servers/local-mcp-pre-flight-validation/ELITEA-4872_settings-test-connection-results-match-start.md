---
id: ELITEA-4872
title: "Verify Settings Test connection results match Start"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed and the tray is running
- A valid baseline configuration with a saved token
- A project the user is not a member of
- Access to the tray log

## Test Data

| Case | Values |
|------|--------|
| All valid | Valid URL, token, project ID |
| UI-link URL | `{{base_url}}/app/13/mcp` |
| Bad host | `https://does-not-exist.invalid` |
| Bad token | `invalid-token-123` |
| No access | Project the user does not belong to |
| Missing project ID | Empty field |
| Token left empty with a saved token | Field empty |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Configuration > Settings... | The Settings window opens |
| 2 | Enter the first case and run **Test connection** | Lines are listed for Deployment URL, Project ID, Platform reachable, Token and Project access, each with a mark and text |
| 3 | Repeat step 2 for every case | Failing cases mark the failing line with a specific message; later dependent lines say they cannot be checked |
| 4 | For each failing case, save the configuration, close the window and select **Start MCP Server** | Start shows the same problem and wording as Test connection |
| 5 | Check the window, the notification and the log | The token is never shown |
| 6 | Run the "Token left empty with a saved token" case | The saved token is used and its result matches the valid case |

## Expected Final State

Test connection and Start report the same problem for the same configuration. The token is never displayed.

## Pass/Fail Criteria

**Pass:**
- All five lines appear with correct marks for each case
- The Start message matches the Test connection result for every failing case
- The token is not visible in the window, notification or log

**Fail:**
- Test connection and Start disagree
- A line is missing or marked wrongly
- The token is exposed anywhere
