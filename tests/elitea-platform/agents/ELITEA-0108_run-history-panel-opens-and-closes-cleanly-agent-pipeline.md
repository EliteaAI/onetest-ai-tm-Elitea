---
id: ELITEA-0108
title: "Run History panel opens and closes cleanly (Agent & Pipeline)"
priority: medium
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:agents, issue:3707, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3707]
---
# ELITEA-0108: Run History panel opens and closes cleanly (Agent & Pipeline)

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Run History panel can be opened and closed without layout issues or broken UI state, for both Agents and Pipelines.

**Coverage:**
- Panel open/close cycle for Agent and Pipeline
- No layout shift or UI breakage after closing

## Preconditions

- Logged in to {{base_url}} with a valid user account
- At least one Agent and one Pipeline exist in the project

## Test Data

- Any existing Agent and Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent/Pipeline page. Open any existing agent/pipeline. | Agent/Pipeline detail page opens. |
| 2 | Click the history/clock icon button in the chat area. | Run History panel opens. |
| 3 | Click the X (Close) button on the panel. | Panel closes. Chat input area is fully visible and functional. No layout shift or broken elements. |
| 4 | Click the history button again. | Panel reopens correctly. |
| 5 | Click the X button again to close. | Panel closes cleanly a second time with no UI breakage. |

## Expected Final State

Panel closes cleanly a second time with no UI breakage.

## Pass/Fail Criteria

**Pass:**
- Panel opens and closes without layout issues for both Agents and Pipelines
- Chat area remains functional after panel is dismissed
- No broken UI state after repeated open/close cycles

**Fail:**
- Panel does not close, or closing it breaks the chat layout
- Chat input or other UI elements become inaccessible after the panel is dismissed
