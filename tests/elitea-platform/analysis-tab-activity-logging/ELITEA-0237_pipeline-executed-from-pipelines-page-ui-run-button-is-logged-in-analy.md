---
id: ELITEA-0237
title: "Pipeline executed from Pipelines page UI (Run button) is logged in Analysis tab"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0237: Pipeline executed from Pipelines page UI (Run button) is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that executing a Pipeline directly from the Pipelines page via the Run button creates a log entry in the Analysis tab.

**Coverage:**
- Pipelines page Run invocation is logged in Analysis tab
- Entry identifies correct pipeline name, version, and timestamp
- Covers the Pipelines page UI invocation surface

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A published Pipeline exists in the current project with a Run button or run panel available on its detail/edit page

## Test Data

- Pipeline run input (if required): `"Pipelines page run — analysis tab test"`
- Pipeline: any published Pipeline in the current project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page from the sidebar. Open the target Pipeline. | Pipeline detail or edit page opens. |
| 2 | Locate the Run panel or Run button. Enter input if required by the pipeline: `"Pipelines page run — analysis tab test"`. | Run panel is accessible and input accepted. |
| 3 | Click Run. Wait for execution to complete. | Pipeline executes and results or output are shown in the run panel. |
| 4 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens with the activity log. |
| 5 | Locate the entry for the Pipelines page run (filter by timestamp or pipeline name). | Entry is present with correct pipeline name, timestamp within 60 seconds, and Pipelines page source. |

## Expected Final State

Entry is present with correct pipeline name, timestamp within 60 seconds, and Pipelines page source.

## Pass/Fail Criteria

**Pass:**
- Pipelines page UI run produces an entry in Analysis tab
- Entry correctly identifies pipeline name and timestamp

**Fail:**
- No entry for the Pipelines page UI run
- Only Chat-triggered pipeline runs are logged
