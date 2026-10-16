---
id: ELITEA-1695
title: "Blocked Tool: Live-Reload and Case-Insensitive Matching"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: automated
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
automation_test_id:
  - tests.ui.admin.test_guardrails_live_reload.TestBlockedToolLiveReload.test_blocked_tool_live_reload_case_insensitive
---
# ELITEA-1695: Blocked Tool: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Blocked Tools changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Other tools in the same toolkit remain functional
4. Unblocking a tool is applied immediately as well

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- A JIRA credential (e.g. `guardrails_test_credential`) with a valid Jira base URL, username and API key
- A JIRA toolkit (e.g. `guardrails_test_jira_toolkit`) using that credential, with tools `list_projects` and `search_using_jql` selected
- An agent (e.g. `guardrails_test_agent`) with the JIRA toolkit attached and saved
- No `jira` / `JIRA` / `Jira` entry in "Blocked Toolkits", and neither `list_projects` nor `search_using_jql` in "Blocked Tools" or "Sensitive Action Tools"

## Test Data

| Toolkit | Tool to Block | Other Tool (should remain working) |
|---------|--------------|------------------------------------|
| `jira` | `search_using_jql` | `list_projects` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `search_using_jql` is NOT in "Blocked Tools" and the "Blocked Tools" field has no "Reload required" badge. | Tool is allowed. **No "Reload required" badge** next to this setting. |
| 3 | Open the agent page and send in the agent chat: "Search for issues in TEST project using JQL query: project = TEST. Execute the tool." | A non-empty response is returned; it does not say the tool is blocked or not available. |
| 4 | Return to Admin UI. In "Blocked Tools", select the `jira` toolkit and add `search_using_jql`. | Tool added to blocked list. |
| 5 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 6 | **WITHOUT reloading pylons**, reload the agent page. | The JIRA toolkit in the agent's Toolkits section shows "Some tools are not available anymore". Change applied immediately. |
| 7 | Send in the agent chat: "List all JIRA projects. Execute the tool." | `list_projects` still works — the response lists/mentions Jira projects. Only `search_using_jql` is blocked. |
| 8 | Return to Admin UI. Remove `search_using_jql` from "Blocked Tools". Save. Reload the agent page. | Configuration saved. The "Some tools are not available anymore" indicator is gone. |

## Expected Final State

Blocked Tools changes are applied immediately. Only the specific tool is blocked; other tools in the toolkit remain functional. `search_using_jql` is no longer in "Blocked Tools".

## Pass/Fail Criteria

**Pass:**
- Blocked Tools changes take effect immediately after save
- No pylon reload required
- No "Reload required" badge on the field
- No yellow banner after save
- Blocking the tool immediately shows "Some tools are not available anymore" on the agent's toolkit
- Only the specific blocked tool is blocked, not the entire toolkit
- Unblocking immediately removes the indicator

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" badge or banner appears
- Blocking one tool affects other tools in the toolkit
- Indicator remains after the tool is unblocked

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP. "Without pylon reload" means no backend restart — refreshing the agent page in the browser is allowed and is how the new state is picked up.

**Coverage note:** the automated flow uses the lowercase `jira` key only; upper/mixed-case variants (`JIRA`, `Jira`) are cleaned up as preconditions but not asserted separately.
