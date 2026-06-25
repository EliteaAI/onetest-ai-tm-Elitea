---
id: ELITEA-1702
title: "Existing Guardrails Enforcement Behavior Not Regressed"
priority: critical
type: regression
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1702: Existing Guardrails Enforcement Behavior Not Regressed

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the case-insensitive matching and live-reload changes do not regress existing Guardrails enforcement behavior. All previously matched tool and toolkit names must continue to be enforced correctly.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- Existing Guardrails configuration with blocked and sensitive tools
- Agents configured with various toolkits

## Test Data

| Existing Config | Tools/Toolkits | Expected Behavior (unchanged) |
|-----------------|---------------|------------------------------|
| Blocked Toolkit | `github` | All github tools blocked |
| Blocked Tool | `jira:delete_issue` | delete_issue blocked, other jira tools work |
| Sensitive Tool | `data_analysis:pandas_analyze_data` | Authorization dialog appears |
| Sensitive Tool | `pyodide:execute_code` | Authorization dialog appears |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. Review existing configuration. | Existing blocked toolkits, blocked tools, and sensitive tools are displayed. |
| 2 | Open agent chat with `github` toolkit (if github is blocked). | Agent chat opens. |
| 3 | Attempt to use any github tool. | Tool is blocked. Same behavior as before the changes. |
| 4 | Open agent chat with `jira` toolkit (if `delete_issue` is blocked). | Agent chat opens. |
| 5 | Attempt to delete an issue. | `delete_issue` is blocked. |
| 6 | Attempt to get an issue. | `get_issue` works normally. |
| 7 | Open agent chat with `data_analysis` toolkit (if `pandas_analyze_data` is sensitive). | Agent chat opens. |
| 8 | Trigger `pandas_analyze_data` tool. | Authorization dialog appears. Same behavior as before. |
| 9 | Authorize and verify execution. | Tool executes with original parameters. Streaming works. |
| 10 | Test `pyodide:execute_code` if configured as sensitive. | Authorization dialog appears for arbitrary code execution. |
| 11 | Verify tool parameters are passed correctly after authorization. | Parameters match what was shown in dialog. |

## Expected Final State

All existing Guardrails enforcement rules continue to work exactly as before. No previously blocked or sensitive tool policy is inadvertently bypassed.

## Pass/Fail Criteria

**Pass:**
- All previously configured blocked toolkits still block all their tools
- All previously configured blocked tools still blocked individually
- All previously configured sensitive tools still trigger authorization dialog
- Tool execution after authorization works correctly with original parameters
- Streaming responses work after authorization
- No enforcement gaps introduced by the changes

**Fail:**
- Previously blocked toolkit or tool now accessible without being unblocked
- Previously sensitive tool executes without authorization dialog
- Authorization dialog content changed unexpectedly
- Tool parameters not passed correctly after authorization
- Any existing Guardrails rule inadvertently bypassed
