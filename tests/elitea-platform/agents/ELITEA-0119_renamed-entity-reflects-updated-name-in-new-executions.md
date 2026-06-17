---
id: ELITEA-0119
title: "Renamed Entity Reflects Updated Name in New Executions"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0119: Renamed Entity Reflects Updated Name in New Executions

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after renaming a Toolkit, new agent executions reflect the updated name in chipsets, while historical runs are not retroactively altered.

**Coverage:**
- Pre-rename execution: chipset shows "Old Tracker: [toolAction]"
- Post-rename execution: chipset shows "New Tracker: [toolAction]"
- Historical run (pre-rename): chipset still shows "Old Tracker: [toolAction]" — history accuracy preserved
- No stale name carried into new runs after rename

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Toolkit configured as "Old Tracker" and used by an Agent
- Agent has History Runs accessible
- Browser: Chrome/Edge latest

## Test Data

- Toolkit original name: "Old Tracker"
- Toolkit renamed to: "New Tracker"
- Test prompt: "Track this task"
- Pre-rename run must be preserved in History Runs for comparison
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Agents and open the target agent. Switch to the Chat or Run tab. Enter a prompt that triggers the Old Tracker toolkit (e.g., 'Track this task'). Press Send. | Agent executes; execution trace shows a chipset for the Old Tracker toolkit. |
| 2 | Open the execution trace panel. Locate the Old Tracker chipset and read its label. | Chipset label reads 'Old Tracker: [toolAction]' — the original toolkit name is shown. |
| 3 | Navigate to Toolkits in the left sidebar. Open the Old Tracker toolkit settings page. | Old Tracker toolkit settings page loads. |
| 4 | Click Edit (or the rename/settings option). Change the toolkit name from 'Old Tracker' to 'New Tracker'. Click Save (or equivalent). | Save succeeds; the toolkit settings page now shows the name 'New Tracker'. |
| 5 | Return to the Agent. Switch to the Chat or Run tab. Enter the same prompt as step 1. Press Send. | Agent executes a new run; this is a fresh execution after the rename. |
| 6 | Wait for execution to complete. Open the execution trace panel for this new run. Locate the toolkit chipset and read its label. | Chipset label reads 'New Tracker: [toolAction]' — the updated name is reflected in the new run. |
| 7 | Navigate to History Runs for the agent. Open the previous run logged in step 1 (before the rename). | Historical run details load. |
| 8 | Locate the toolkit chipset in the historical run's execution trace. Read its label. | Historical run chipset still shows 'Old Tracker: [toolAction]' — the old name is preserved in history; no retroactive change. |

## Expected Final State

Historical run chipset still shows 'Old Tracker: [toolAction]' — the old name is preserved in history; no retroactive change.

## Pass/Fail Criteria

**Pass:**
- New execution chipset reflects renamed toolkit name "New Tracker"
- Historical run chipset still shows original name "Old Tracker"
- Old history is not retroactively altered

**Fail:**
- New execution still shows the old name "Old Tracker"
- Historical run has been retroactively updated to show "New Tracker" (history corrupted)
