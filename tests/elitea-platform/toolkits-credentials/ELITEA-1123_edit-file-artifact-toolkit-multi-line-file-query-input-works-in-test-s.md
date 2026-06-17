---
id: ELITEA-1123
title: "Edit File (Artifact Toolkit): Multi-line File Query Input Works in Test Settings"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, eng:frontend, eng:backend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3528]
---
# ELITEA-1123: Edit File (Artifact Toolkit): Multi-line File Query Input Works in Test Settings

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a multi-line File Query can be entered and the `edit_file` tool in the Artifact toolkit executes successfully from the Toolkit Test Settings panel.

**Coverage:**
- Multi-line text entry accepted in File Query field in Artifact toolkit Test Settings
- `edit_file` tool executes without marker parsing errors
- Artifact file content is updated as expected

## Preconditions

- Logged into ELITEA at {{base_url}}
- Configured **Artifact** toolkit with `edit_file` tool enabled
- A test artifact file exists containing the text: `original artifact content`

## Test Data

Toolkit: Artifact
Tool: Edit File

File path: path to the test artifact file (e.g., test/edit-test.txt)
File Query (enter each line separately, do NOT paste as single line):
OLD <<<<
original artifact content
>>>> OLD
NEW <<<<
updated artifact content
>>>> NEW

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits and open the configured Artifact toolkit. Open the Test Settings panel. | Test Settings panel opens. |
| 2 | From the tool dropdown, select 'Edit File'. | Parameter fields load including File Query * and any required file path/reference fields. |
| 3 | Enter valid values for all required fields (file path and any artifact reference fields). | Values are set. |
| 4 | Click inside the File Query * field. Type the 6-line OLD/NEW block pressing Enter between each line: 'OLD <<<<' [Enter] 'original artifact content' [Enter] '>>>> OLD' [Enter] 'NEW <<<<' [Enter] 'updated artifact content' [Enter] '>>>> NEW'. | All 6 lines appear in the field on separate rows. Pressing Enter does not navigate away or submit the form. |
| 5 | Click RUN TOOL. Wait for the response. | Response does NOT contain a marker parsing error. Response indicates successful file edit. |

## Expected Final State

Response does NOT contain a marker parsing error. Response indicates successful file edit.

## Pass/Fail Criteria

**Pass:**
- Multi-line File Query is accepted in the Artifact toolkit's Test Settings
- `edit_file` executes and returns a success response without marker parsing errors
- Artifact file content is updated as expected

**Fail:**
- File Query * field collapses input or triggers navigation on Enter
- Marker parsing error is returned in the response
- Tool returns success but artifact content is unchanged
