---
id: ELITEA-0107
title: "History button is visible and accessible in the chat area for Agents and Pipelines"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:agents, issue:3707, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3707]
---
# ELITEA-0107: History button is visible and accessible in the chat area for Agents and Pipelines

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the history/clock icon button is present in the top-right of the chat panel for both Agents and Pipelines, and that clicking it opens the Run History panel.

**Coverage:**
- History button presence on Agent/Pipeline detail page
- Clicking the button opens the Run History panel for both entity types
- Configuration and History tabs are absent from the page header

## Preconditions

- Logged in to {{base_url}} with a valid user account
- At least one Agent and one Pipeline exist in the project with at least one prior execution

## Test Data

- Any existing Agent and Pipeline with at least one prior execution

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent/Pipeline page. Open any existing agent/pipeline. | Agent/Pipeline detail page opens. |
| 2 | Inspect the page header top bar. | No "Configuration" tab and no "History" tab are present in the header navigation. |
| 3 | Locate the top-right area of the chat panel. | A history/clock icon button is visible. |
| 4 | Click the history/clock icon button. | The Run History panel opens. |

## Expected Final State

The Run History panel opens.

## Pass/Fail Criteria

**Pass:**
- History/clock icon button is present in the chat area for both Agents and Pipelines
- Clicking it opens the Run History panel in both cases
- No Configuration or History tabs exist in the header

**Fail:**
- History button is missing from the chat area for either entity type
- Clicking the button does not open the Run History panel
- Configuration or History tabs still appear in the header
