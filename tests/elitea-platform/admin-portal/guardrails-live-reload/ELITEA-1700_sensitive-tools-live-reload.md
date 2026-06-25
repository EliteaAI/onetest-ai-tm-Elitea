---
id: ELITEA-1700
title: "Guardrails Sensitive Action Tools Changes Apply Immediately Without Pylon Reload"
priority: critical
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1700: Guardrails Sensitive Action Tools Changes Apply Immediately Without Pylon Reload

**Module:** Admin Portal / Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changes to Sensitive Action Tools configuration take effect immediately at runtime after an admin saves changes, without requiring a pylon reload or restart.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent configured with access to a toolkit where specific tools can be marked as sensitive
- Agent is actively usable

## Test Data

| Toolkit | Tool to Mark Sensitive | Expected Behavior After |
|---------|----------------------|-------------------------|
| `data_analysis` | `pandas_analyze_data` | Authorization dialog appears |
| `github` | `create_pull_request` | Authorization dialog appears |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Verify `pandas_analyze_data` under `data_analysis` is NOT in "Sensitive Action Tools". | Tool executes without authorization. |
| 3 | Open agent chat with `data_analysis` toolkit enabled. | Agent chat opens. |
| 4 | Send prompt that triggers `pandas_analyze_data` tool. | Tool executes immediately WITHOUT authorization dialog. |
| 5 | Return to Admin UI. In "Sensitive Action Tools", add `pandas_analyze_data` under `data_analysis`. | Tool added to sensitive list. |
| 6 | Click "Save Configuration". | Configuration saved. **No "Reload required" banner for this setting.** |
| 7 | **WITHOUT reloading pylons**, return to agent chat. | Agent chat still open. |
| 8 | Send prompt that triggers `pandas_analyze_data` tool again. | Authorization dialog NOW APPEARS. Sensitive rule applied immediately. |
| 9 | Click "Authorize" in dialog. | Tool executes after authorization. |
| 10 | Return to Admin UI. Remove `pandas_analyze_data` from Sensitive Action Tools. Save. | Configuration saved. |
| 11 | Return to agent chat. Trigger `pandas_analyze_data` again. | Tool executes immediately without authorization dialog. |

## Expected Final State

Sensitive Action Tools changes are applied immediately. Authorization dialog behavior changes without pylon restart.

## Pass/Fail Criteria

**Pass:**
- Sensitive Action Tools changes take effect immediately after save
- No pylon reload required
- Adding a tool to sensitive list immediately triggers authorization dialog
- Removing a tool from sensitive list immediately removes authorization requirement
- No "Reload required" banner shown for Sensitive Action Tools setting

**Fail:**
- Changes require pylon reload to take effect
- "Reload required" banner appears for Sensitive Action Tools
- Authorization dialog behavior doesn't change until restart
- Inconsistent behavior between adding and removing sensitive tools
