---
id: ELITEA-1696
title: "Sensitive Tool: Live-Reload and Case-Insensitive Matching"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: automated
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
automation_test_id:
  - tests.ui.admin.test_guardrails_live_reload.TestSensitiveToolLiveReload.test_sensitive_tool_live_reload_case_insensitive
---
# ELITEA-1696: Sensitive Tool: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Sensitive Action Tools changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Authorization panel appears/disappears immediately after config change

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- A JIRA credential (e.g. `guardrails_test_credential`) with a valid Jira base URL, username and API key
- A JIRA toolkit (e.g. `guardrails_test_jira_toolkit`) using that credential, with tools `list_projects` and `search_using_jql` selected
- An agent (e.g. `guardrails_test_agent`) with the JIRA toolkit attached and saved
- No `jira` / `JIRA` / `Jira` entry in "Blocked Toolkits", and neither `list_projects` nor `search_using_jql` in "Blocked Tools" or "Sensitive Action Tools"

## Test Data

| Toolkit | Tool to Mark Sensitive | Prompt | Expected Behavior After |
|---------|----------------------|--------|-------------------------|
| `jira` | `list_projects` | "List all JIRA projects available. Execute the tool." | Sensitive Action Authorization panel appears |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `list_projects` under `jira` is NOT in "Sensitive Action Tools" and the field has no "Reload required" badge. | Tool is not sensitive. **No "Reload required" badge** next to this setting. |
| 3 | Open the agent page and send in the agent chat: "List all JIRA projects available. Execute the tool." | Tool executes WITHOUT any authorization/approval prompt; a non-empty response is returned. |
| 4 | Return to Admin UI. In "Sensitive Action Tools", select the `jira` toolkit and add `list_projects`. | Tool added to sensitive list. |
| 5 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 6 | **WITHOUT reloading pylons**, reload the agent page and send the same prompt. | The Sensitive Action Authorization panel NOW APPEARS. Change applied immediately. |
| 7 | Click "Authorize" in the panel. | Tool executes and the response completes. |
| 8 | Return to Admin UI. Remove `list_projects` from "Sensitive Action Tools". Save. Return to the agent and send the same prompt. | Configuration saved. Tool executes without the authorization panel. |

## Expected Final State

Sensitive Action Tools changes are applied immediately. Authorization panel behavior changes without pylon restart. `list_projects` is no longer in "Sensitive Action Tools".

## Pass/Fail Criteria

**Pass:**
- Sensitive Action Tools changes take effect immediately after save
- No pylon reload required
- No "Reload required" badge on the field
- No yellow banner after save
- Adding the tool to the sensitive list immediately triggers the authorization panel
- Authorizing lets the tool run to completion
- Removing the tool from the sensitive list immediately removes the authorization requirement

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" badge or banner appears
- Authorization panel behavior doesn't change until restart

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP. "Without pylon reload" means no backend restart — refreshing the agent page in the browser is allowed and is how the new state is picked up.

**Coverage note:** the automated flow uses the lowercase `jira` key only; upper/mixed-case variants (`JIRA`, `Jira`) are cleaned up as preconditions but not asserted separately.
