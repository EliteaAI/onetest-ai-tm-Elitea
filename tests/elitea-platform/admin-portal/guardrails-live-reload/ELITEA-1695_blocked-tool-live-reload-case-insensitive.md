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
---
# ELITEA-1695: Blocked Tool: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Blocked Tools changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Case-insensitive matching works correctly
4. Other tools in the same toolkit remain functional

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent with access to a toolkit containing tools to be blocked (e.g., `github` toolkit with `create_pull_request` tool)
- Agent is actively usable

## Test Data

| Toolkit | Tool to Block | Other Tools (should remain working) |
|---------|--------------|-------------------------------------|
| `github` | `get_issue` | `list_repos`, `create_pull_request` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `get_issue` tool under `github` toolkit is NOT in "Blocked Tools". | Tool is allowed. |
| 3 | Verify that the "Blocked Tools" field does NOT have a "Reload required" badge. | **No "Reload required" badge** next to this setting. |
| 4 | Open agent chat with `github` toolkit enabled. | Agent chat opens. |
| 5 | Send a prompt: "Create a pull request for my changes". | `get_issue` tool executes (or attempts to). Tool is accessible. |
| 6 | Return to Admin UI. In "Blocked Tools", select `github` toolkit and add `get_issue`. | Tool added to blocked list. |
| 7 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 8 | **WITHOUT reloading pylons**, return to agent chat. | Agent chat still open. |
| 9 | Send the same prompt again. | `get_issue` tool is BLOCKED. Message: "Some tools are not available anymore." Change applied immediately. |
| 10 | Send prompt: "List my repositories". | `list_repos` tool still works. Only `get_issue` is blocked. |
| 11 | Verify case-insensitive matching works (`get_issue`, `Get_Issue`, `GET_ISSUE`). | All casing variants are blocked. |
| 12 | Return to Admin UI. Remove `get_issue` from blocked tools. Save. | Configuration saved. |
| 13 | Return to agent chat. Attempt to create pull request again. | `get_issue` tool now accessible again. |

## Expected Final State

Blocked Tools changes are applied immediately with case-insensitive matching. Only the specific tool is blocked, other tools in the toolkit remain functional.

## Pass/Fail Criteria

**Pass:**
- Blocked Tools changes take effect immediately after save
- No pylon reload required
- No "Reload required" badge on the field
- No yellow banner after save
- Only the specific blocked tool is blocked, not the entire toolkit
- Unblocking restores tool access immediately
- Case-insensitive matching works for all naming variants

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" badge or banner appears
- Blocking one tool affects other tools in the toolkit
- Case-sensitive matching allows some variants to execute

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP.
