---
id: ELITEA-1126
title: "Edit File (Artifact Toolkit): Multi-line File Query Input Works in Pipeline Toolkit Node"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, eng:frontend, eng:backend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3528]
---
# ELITEA-1126: Edit File (Artifact Toolkit): Multi-line File Query Input Works in Pipeline Toolkit Node

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a multi-line File Query can be entered in a Pipeline Toolkit Node and the `edit_file` tool in the Artifact toolkit executes successfully end-to-end.

**Coverage:**
- Multi-line text entry accepted in File Query field in Artifact toolkit Pipeline Toolkit Node
- Pipeline run completes without marker parsing errors
- Artifact file content is updated successfully via pipeline execution

## Preconditions

- Logged into ELITEA at {{base_url}}
- A pipeline exists with a Toolkit Node configured with the **Artifact** toolkit's `edit_file` tool
- The target artifact file contains the text: `original artifact content`

## Test Data

Toolkit: Artifact
Tool: Edit File

File path: path to the test artifact file (e.g., test/edit-test.txt)
File Query (enter each line separately, do NOT paste as single line):
"
OLD <<<<
original artifact content
>>>> OLD
NEW <<<<
updated artifact content
>>>> NEW
"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline containing the Artifact toolkit Edit File Toolkit Node. Click the node to open its configuration panel. | Node configuration panel opens with parameter fields visible, including File Query field. |
| 2 | Enter valid values for all required node parameters (file path and any artifact reference fields). | Values are set. |
| 3 | Click inside the File Query field. Type the 6-line OLD/NEW block pressing Enter between each line: 'OLD <<<<' [Enter] 'original artifact content' [Enter] '>>>> OLD' [Enter] 'NEW <<<<' [Enter] 'updated artifact content' [Enter] '>>>> NEW'. | All 6 lines appear in the field with line breaks visible. Enter does not submit the form or close the panel. |
| 4 | Save the pipeline. | Pipeline saves without errors. |
| 5 | Run the pipeline. Wait for execution to complete. | Pipeline run completes. |
| 6 | Inspect the Edit File node output in the run result. | Output does NOT contain a marker parsing error. Node reports successful file edit. |

## Expected Final State

Output does NOT contain a marker parsing error. Node reports successful file edit.

## Pass/Fail Criteria

**Pass:**
- Multi-line File Query is accepted in the Artifact toolkit's Pipeline Toolkit Node
- Pipeline run completes without marker parsing errors
- Artifact file content is updated as expected

**Fail:**
- File Query field collapses input or triggers navigation on Enter in the node configuration
- Marker parsing error appears in the pipeline run output
- Tool returns success but artifact content is unchanged
