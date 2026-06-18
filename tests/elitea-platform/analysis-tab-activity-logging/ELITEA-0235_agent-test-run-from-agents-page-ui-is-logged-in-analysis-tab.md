---
id: ELITEA-0235
title: "Agent test-run from Agents page UI is logged in Analysis tab"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0235: Agent test-run from Agents page UI is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that executing an Agent via the test/run panel on the Agents page creates a corresponding entry in the Analysis tab.

**Coverage:**
- Agents page UI test run logged in Analysis tab
- Log entry correctly identifies the agent, version, and execution timestamp
- All 4 invocation surfaces produce consistent logging behavior (this covers the Agents page UI surface)

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A published Agent exists in the current project
- The Agent has a test/run panel accessible from its detail/edit page

## Test Data

- Agent test input: `"Agents page UI run — analysis tab test"`
- Agent: any published Agent in the current project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page from the sidebar. Open the target Agent. | Agent detail or edit page opens. |
| 2 | Locate the test panel (typically on the right side or bottom of the page). Enter input: `"Agents page UI run — analysis tab test"`. | Input is accepted in the test panel. |
| 3 | Click the Run / Send button in the test panel. | Agent generates a response visible in the test panel. |
| 4 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens with the activity log. |
| 5 | Locate the entry for the Agents page test run (filter by timestamp or agent name). | Entry is present with correct agent name, timestamp within 60 seconds of the run, and Agents page / UI source. |

## Expected Final State

Entry is present with correct agent name, timestamp within 60 seconds of the run, and Agents page / UI source.

## Pass/Fail Criteria

**Pass:**
- UI test run from Agents page produces an entry in Analysis tab
- Entry timestamp and agent identity match the test run

**Fail:**
- No entry visible for the Agents page UI test run
- Only Chat-sourced agent calls are logged
