---
id: ELITEA-3746
title: "Blocked Toolkit: Live-Reload and Case-Insensitive Matching"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: automated
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
automation_test_id:
  - tests.ui.admin.test_guardrails_live_reload.TestBlockedToolkitLiveReload.test_blocked_toolkit_live_reload_case_insensitive
---
# ELITEA-3746: Blocked Toolkit: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Blocked Toolkits changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Unblocking a toolkit is applied immediately as well

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- A JIRA credential (e.g. `guardrails_test_credential`) with a valid Jira base URL, username and API key
- A JIRA toolkit (e.g. `guardrails_test_jira_toolkit`) using that credential, with tools `list_projects` and `search_using_jql` selected
- An agent (e.g. `guardrails_test_agent`) with the JIRA toolkit attached and saved
- No `jira` / `JIRA` / `Jira` entry in "Blocked Toolkits", and neither `list_projects` nor `search_using_jql` in "Blocked Tools" or "Sensitive Action Tools"

## Test Data

| Toolkit to Block | Agent to Test | Prompt |
|-----------------|---------------|--------|
| `jira` | Agent with the JIRA toolkit | "List all JIRA projects available. Execute the tool." |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `jira` toolkit is NOT in "Blocked Toolkits" and the "Blocked Toolkits" field has no "Reload required" badge. | Toolkit is allowed. **No "Reload required" badge** next to this setting. |
| 3 | Open the agent page and send in the agent chat: "List all JIRA projects available. Execute the tool." | A non-empty response is returned; it does not say the tool is blocked or can't run. |
| 4 | Return to Admin UI. Add `jira` to "Blocked Toolkits". | Toolkit added to blocked list. |
| 5 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 6 | **WITHOUT reloading pylons**, reload the agent page. | The JIRA toolkit in the agent's Toolkits section shows the "blocked by your organization" indicator. Change applied immediately. |
| 7 | Return to Admin UI. Remove `jira` from "Blocked Toolkits". Save. Reload the agent page. | Configuration saved. The "blocked by your organization" indicator is gone. Unblocking also applied immediately. |

## Expected Final State

Blocked Toolkits changes are applied immediately at runtime. No pylon restart required. `jira` is no longer in "Blocked Toolkits".

## Pass/Fail Criteria

**Pass:**
- Blocked Toolkits changes take effect immediately after save
- No pylon reload required for changes to apply
- No "Reload required" badge on the field
- No yellow banner after save
- Blocking the toolkit immediately marks it "blocked by your organization" on the agent
- Unblocking the toolkit immediately removes the blocked indicator

**Fail:**
- Changes only apply after pylon reload
- "Reload required" badge or banner appears
- Toolkit is not marked blocked on the agent after being added to the blocked list
- Blocked indicator remains after the toolkit is removed from the blocked list

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP. "Without pylon reload" means no backend restart — refreshing the agent page in the browser is allowed and is how the new state is picked up.

**Coverage note:** the automated flow uses the lowercase `jira` key only; upper/mixed-case variants (`JIRA`, `Jira`) are cleaned up as preconditions but not asserted separately.
