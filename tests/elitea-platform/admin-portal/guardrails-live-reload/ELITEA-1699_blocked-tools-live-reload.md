---
id: ELITEA-1699
title: "Guardrails Blocked Tools Changes Apply Immediately Without Pylon Reload"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1699: Guardrails Blocked Tools Changes Apply Immediately Without Pylon Reload

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changes to Blocked Tools configuration take effect immediately at runtime after an admin saves changes, without requiring a pylon reload or restart.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent configured with access to a toolkit (e.g., `github`) where specific tools can be blocked
- Agent is actively usable

## Test Data

| Toolkit | Tool to Block | Other Tools (should remain working) |
|---------|--------------|-------------------------------------|
| `github` | `delete_branch` | `list_repos`, `create_pull_request` |
| `jira` | `delete_issue` | `get_issue`, `create_issue` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `delete_branch` tool under `github` toolkit is NOT in "Blocked Tools". | Tool is allowed. |
| 3 | Open agent chat with `github` toolkit enabled. | Agent chat opens. |
| 4 | Send prompt: "Delete the feature-test branch from my repo". | `delete_branch` tool executes (or would execute if branch exists). Tool is accessible. |
| 5 | Return to Admin UI. In "Blocked Tools", select `github` toolkit and add `delete_branch`. | Tool added to blocked list. |
| 6 | Click "Save Configuration". | Configuration saved. **No "Reload required" banner for this setting.** |
| 7 | **WITHOUT reloading pylons**, return to agent chat. | Agent chat still open. |
| 8 | Send prompt: "Delete the feature-test branch". | `delete_branch` tool is BLOCKED. Agent acknowledges it cannot perform this action. |
| 9 | Send prompt: "List my repositories". | `list_repos` tool still works. Only `delete_branch` is blocked. |
| 10 | Return to Admin UI. Remove `delete_branch` from blocked tools. Save. | Configuration saved. |
| 11 | Return to agent chat. Attempt to delete branch again. | `delete_branch` tool now accessible again. |

## Expected Final State

Blocked Tools changes are applied immediately. Specific tools are blocked/unblocked without pylon restart while other tools in the same toolkit remain unaffected.

## Pass/Fail Criteria

**Pass:**
- Blocked Tools changes take effect immediately after save
- No pylon reload required
- Only the specific blocked tool is blocked, not the entire toolkit
- Unblocking restores tool access immediately
- No "Reload required" banner shown for Blocked Tools setting

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" banner appears for Blocked Tools
- Blocking one tool affects other tools in the toolkit
- Changes not reflected immediately at runtime
