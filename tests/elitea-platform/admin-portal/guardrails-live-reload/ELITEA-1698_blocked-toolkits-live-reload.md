---
id: ELITEA-1698
title: "Guardrails Blocked Toolkits Changes Apply Immediately Without Pylon Reload"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1698: Guardrails Blocked Toolkits Changes Apply Immediately Without Pylon Reload

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changes to Blocked Toolkits configuration take effect immediately at runtime after an admin saves changes, without requiring a pylon reload or restart.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent configured with access to a toolkit (e.g., `github`) that can be blocked
- Agent is actively usable (not requiring pylon restart to function)

## Test Data

| Toolkit to Block | Agent to Test | Tool to Invoke |
|-----------------|---------------|----------------|
| `github` | Any agent with github toolkit | `list_repos` |
| `jira` | Any agent with jira toolkit | `get_issue` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `github` toolkit is NOT in "Blocked Toolkits". | Github toolkit is allowed. |
| 3 | Open a new browser tab with an agent chat that has `github` toolkit enabled. | Agent chat opens. |
| 4 | Send prompt: "List my GitHub repositories". | `list_repos` tool executes successfully. Repositories are listed. |
| 5 | Return to Admin UI tab. Add `github` to "Blocked Toolkits". | Toolkit added to blocked list. |
| 6 | Click "Save Configuration". | Configuration saved successfully. **No "Reload required" banner appears for this setting.** |
| 7 | **WITHOUT reloading pylons**, return to agent chat tab. | Agent chat still open. |
| 8 | Send prompt: "List my GitHub repositories" again. | `list_repos` tool is now BLOCKED. Agent cannot use github toolkit. Change applied immediately. |
| 9 | Return to Admin UI. Remove `github` from "Blocked Toolkits". Save. | Configuration saved. |
| 10 | Return to agent chat. Send same prompt. | `list_repos` tool executes successfully again. Unblocking also applied immediately. |

## Expected Final State

Blocked Toolkits changes are applied immediately at runtime. The toolkit is blocked/unblocked without any pylon restart.

## Pass/Fail Criteria

**Pass:**
- Blocked Toolkits changes take effect immediately after save
- No pylon reload required for changes to apply
- Blocking a toolkit immediately prevents tool execution
- Unblocking a toolkit immediately restores tool access
- No "Reload required" banner shown for Blocked Toolkits setting

**Fail:**
- Changes only apply after pylon reload
- "Reload required" banner still appears for Blocked Toolkits
- Toolkit remains accessible after being added to blocked list (without restart)
- Inconsistent application of changes across different pylons
