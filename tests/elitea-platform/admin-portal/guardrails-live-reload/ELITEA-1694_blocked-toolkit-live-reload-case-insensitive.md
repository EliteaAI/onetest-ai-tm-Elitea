---
id: ELITEA-1694
title: "Blocked Toolkit: Live-Reload and Case-Insensitive Matching"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1694: Blocked Toolkit: Live-Reload and Case-Insensitive Matching

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that:
1. Blocked Toolkits changes apply immediately without pylon reload
2. No "Reload required" badge or banner is shown
3. Case-insensitive matching works correctly

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent configured with a built-in toolkit (e.g., `pptx`) that can be blocked
- Agent is actively usable

## Test Data

| Toolkit to Block | Agent to Test | Tool to Invoke |
|-----------------|---------------|----------------|
| `pptx` | Any agent with pptx toolkit | Any pptx tool |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `pptx` toolkit is NOT in "Blocked Toolkits". | Toolkit is allowed. |
| 3 | Verify that the "Blocked Toolkits" field does NOT have a "Reload required" badge. | **No "Reload required" badge** next to this setting. |
| 4 | Open a new browser tab with an agent chat that has `pptx` toolkit enabled. | Agent chat opens. |
| 5 | Send a prompt that triggers a tool from `pptx` toolkit. | Tool executes successfully. |
| 6 | Return to Admin UI. Add `pptx` to "Blocked Toolkits". | Toolkit added to blocked list. |
| 7 | Click "Save Configuration". | Configuration saved. **No yellow banner** mentioning pylon reload. |
| 8 | **WITHOUT reloading pylons**, return to agent chat tab. | Agent chat still open. |
| 9 | Send the same prompt again. | Tool is now BLOCKED. Message: "Pptx toolkit is blocked by your organization." Change applied immediately. |
| 10 | Verify case-insensitive matching: blocking works regardless of internal casing (`pptx`, `PPTX`, `PPTx`). | All casing variants are blocked. |
| 11 | Return to Admin UI. Remove `pptx` from "Blocked Toolkits". Save. | Configuration saved. |
| 12 | Return to agent chat. Send same prompt. | Tool executes successfully again. Unblocking also applied immediately. |

## Expected Final State

Blocked Toolkits changes are applied immediately at runtime with case-insensitive matching. No pylon restart required.

## Pass/Fail Criteria

**Pass:**
- Blocked Toolkits changes take effect immediately after save
- No pylon reload required for changes to apply
- No "Reload required" badge on the field
- No yellow banner after save
- Blocking a toolkit immediately prevents tool execution
- Unblocking a toolkit immediately restores tool access
- Case-insensitive matching works (`pptx`, `PPTX`, `PPTx` all blocked)

**Fail:**
- Changes only apply after pylon reload
- "Reload required" badge or banner still appears
- Toolkit remains accessible after being added to blocked list
- Case-sensitive matching allows some variants to bypass blocking

**Note:** Guardrails (Blocked/Sensitive) apply only to built-in toolkits, not to MCP.
