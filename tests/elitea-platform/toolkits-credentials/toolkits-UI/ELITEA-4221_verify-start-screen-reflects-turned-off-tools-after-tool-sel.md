---
id: ELITEA-4221
title: "Verify start screen reflects turned-off tools after tool selection is saved"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4221: Verify start screen reflects turned-off tools after tool selection is saved

## Preconditions

- User is logged in to `{{base_url}}` with edit rights on the toolkit
- Private project is selected
- Toolkit `Jira_Management` exists with all 23 tools enabled

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | `Jira_Management` |
| Tools to turn off (step 1) | Any 2 tools, e.g. `Get issue`, `Add comments` |
| Tool to keep (step 4) | `Search using JQL` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `Jira_Management`, turn off `Get issue` and `Add comments`, and click **Save**. | The toolkit is saved; the counter shows `21 / 23`. |
| 2 | Click **Test**. | The start screen opens. |
| 3 | Look at the tool buttons and open the **Tool** dropdown. | `Get issue` and `Add comments` are not shown on the start screen, matching the Tool dropdown. |
| 4 | Go back to the Config tab, turn off all tools except `Search using JQL`, and click **Save**. | The toolkit is saved; the counter shows `1 / 23`. |
| 5 | Click **Test**. | The start screen shows only `Search using JQL`. |
| 6 | Go back to the Config tab, turn off all tools, and click **Save**. | The toolkit is saved; the counter shows `0 / 23`. |
| 7 | Click **Test**. | The start screen shows all of the toolkit's tools. |
| 8 | Go back to the Config tab, turn all tools on, and click **Save**. | The toolkit is saved; the counter shows `23 / 23`. |

## Expected Final State

The start screen shows only the enabled tools, or all tools when none are enabled. The toolkit is restored with all 23 tools enabled.

## Pass/Fail Criteria

**Pass:**
- Turned-off tools are hidden on the start screen when some tools are enabled
- Only the single enabled tool is shown when one tool is enabled
- All tools are shown when all tools are turned off

**Fail:**
- Turned-off tools are shown while other tools are enabled
- The start screen and the Tool dropdown show different tools
- The page crashes or shows an empty list when all tools are turned off
