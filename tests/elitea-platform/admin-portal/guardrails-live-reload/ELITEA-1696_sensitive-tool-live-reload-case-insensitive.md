---
id: ELITEA-1696
title: "Sensitive Tool: Live-Reload and Case-Insensitive Matching"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1696: Sensitive Tool: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Sensitive Action Tools changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Case-insensitive matching works correctly
4. Authorization dialog appears/disappears immediately after config change

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent with access to a toolkit containing tools to be marked as sensitive (e.g., `github` toolkit with `get_issue` tool)
- Agent is actively usable

## Test Data

| Toolkit | Tool to Mark Sensitive | Expected Behavior After |
|---------|----------------------|-------------------------|
| `github` | `get_issue` | Authorization dialog appears |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `get_issue` under `github` is NOT in "Sensitive Action Tools". | Tool executes without authorization. |
| 3 | Verify that the "Sensitive Action Tools" field does NOT have a "Reload required" badge. | **No "Reload required" badge** next to this setting. |
| 4 | Open agent chat with `github` toolkit enabled. | Agent chat opens. |
| 5 | Send a prompt that triggers `get_issue` tool. | Tool executes immediately WITHOUT authorization dialog. |
| 6 | Return to Admin UI. In "Sensitive Action Tools", select `github` toolkit and mark `get_issue` as sensitive. | Tool added to sensitive list. |
| 7 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 8 | **WITHOUT reloading pylons**, return to agent chat. | Agent chat still open. |
| 9 | Send the same prompt again. | Authorization dialog NOW APPEARS. Change applied immediately. |
| 10 | Click "Authorize" in the dialog. | Tool executes successfully. |
| 11 | Trigger `get_issue` again. Click "Block" in the dialog. | Tool stops execution. Message "...tool was blocked because this specific call wasn't approved" appears. |
| 12 | Verify case-insensitive matching works (`get_issue`, `GET_ISSUE`, `Get_Issue`). | All casing variants trigger authorization dialog. |
| 13 | Return to Admin UI. Remove `get_issue` from Sensitive Action Tools. Save. | Configuration saved. |
| 14 | Return to agent chat. Trigger `get_issue` again. | Tool executes immediately without authorization dialog. |

## Expected Final State

Sensitive Action Tools changes are applied immediately with case-insensitive matching. Authorization dialog behavior changes without pylon restart.

## Pass/Fail Criteria

**Pass:**
- Sensitive Action Tools changes take effect immediately after save
- No pylon reload required
- No "Reload required" badge on the field
- No yellow banner after save
- Adding a tool to sensitive list immediately triggers authorization dialog
- Removing a tool from sensitive list immediately removes authorization requirement
- Case-insensitive matching works for all naming variants

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" badge or banner appears
- Authorization dialog behavior doesn't change until restart
- Case-sensitive matching allows some variants to bypass authorization

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP.
