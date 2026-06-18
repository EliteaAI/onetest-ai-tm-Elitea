---
id: ELITEA-1124
title: "Update File: Multi-line File Query Input Works in Pipeline Toolkit Node"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, int:ado-repos, eng:frontend, eng:backend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3528]
---
# ELITEA-1124: Update File: Multi-line File Query Input Works in Pipeline Toolkit Node

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a multi-line File Query can be entered in a Pipeline Toolkit Node and the `update_file` tool executes successfully end-to-end across all repository toolkit types.

**Coverage:**
- Multi-line text entry accepted in File Query field in Pipeline Toolkit Node (ADO Repos, GitHub, GitLab, GitLab Org, Bitbucket)
- Pipeline run completes without "No OLD/NEW marker pairs found" error
- File is updated successfully via pipeline execution

## Preconditions

- Logged into ELITEA at {{base_url}}
- A pipeline exists with an Update File Toolkit Node configured for each of the 5 toolkit types: **ADO Repos**, **GitHub**, **GitLab**, **GitLab Org**, **Bitbucket**
- Each toolkit's repository has `test-branch` with `test/update-test.txt` containing: `original text to replace`

## Test Data

Toolkits to test (parametrized — repeat steps for each):
| Toolkit Type | Pipeline Node |
|---|---|
| ADO Repos | Update File Toolkit Node (ADO Repos) |
| GitHub | Update File Toolkit Node (GitHub) |
| GitLab | Update File Toolkit Node (GitLab) |
| GitLab Org | Update File Toolkit Node (GitLab Org) |
| Bitbucket | Update File Toolkit Node (Bitbucket) |

File Path: test/update-test.txt
Branch Name: test-branch
File Query (enter each line separately, do NOT paste as single line):
OLD <<<<
original text to replace
>>>> OLD
NEW <<<<
replacement text
>>>> NEW

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline with the ADO Repos Update File Toolkit Node. Click the node to open its configuration panel. | Node configuration panel opens with parameter fields visible. |
| 2 | Enter 'test/update-test.txt' in File Path and 'test-branch' in Branch Name. | Values are set. |
| 3 | Click inside the File Query field. Type the 6-line OLD/NEW block pressing Enter between each line: 'OLD <<<<' [Enter] 'original text to replace' [Enter] '>>>> OLD' [Enter] 'NEW <<<<' [Enter] 'replacement text' [Enter] '>>>> NEW'. | All 6 lines appear in the field with line breaks visible. Enter does not submit the form or close the panel. |
| 4 | Save the pipeline. | Pipeline saves without errors. |
| 5 | Run the pipeline. Wait for execution to complete. | Pipeline run completes. |
| 6 | Inspect the Update File node output in the run result. | Output does NOT contain 'No OLD/NEW marker pairs found in file_query'. Node reports successful file update. |
| 7 | Repeat steps 1–6 for each remaining toolkit type: GitHub, GitLab, GitLab Org, Bitbucket. | All 5 toolkit types accept multi-line input in the pipeline node and complete the run with a success result. |

## Expected Final State

All 5 toolkit types accept multi-line input in the pipeline node and complete the run with a success result.

## Pass/Fail Criteria

**Pass:**
- Multi-line File Query is accepted in the Pipeline Toolkit Node for all 5 toolkit types (ADO Repos, GitHub, GitLab, GitLab Org, Bitbucket)
- Pipeline run completes without the marker error for all 5 toolkit types
- File update is confirmed successful for each toolkit

**Fail:**
- Any toolkit type's File Query field collapses input or triggers navigation on Enter in the node configuration
- "No OLD/NEW marker pairs found in file_query..." error appears in the pipeline run output for any toolkit type
