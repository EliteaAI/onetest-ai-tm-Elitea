---
id: ELITEA-1125
title: "Update File: Multi-line File Query Input Works in Test Settings"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:frontend, eng:backend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3528]
---
# ELITEA-1125: Update File: Multi-line File Query Input Works in Test Settings

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a multi-line File Query can be entered and the `update_file` tool executes successfully from the Toolkit Test Settings panel across all repository toolkit types.

**Coverage:**
- Multi-line text entry accepted in File Query field in Test Settings (ADO Repos, GitHub, GitLab, GitLab Org, Bitbucket)
- Tool executes without "No OLD/NEW marker pairs found" error
- File is updated successfully in the repository

## Preconditions

- Logged into ELITEA at {{base_url}}
- Configured and authenticated instances of all 5 toolkit types with `update_file` enabled: **ADO Repos**, **GitHub**, **GitLab**, **GitLab Org**, **Bitbucket**
- Each toolkit has a test repository with a `test-branch` branch containing `test/update-test.txt` with text: `original text to replace`

## Test Data

Toolkits to test (parametrized — repeat steps for each):
| Toolkit Type | Tool |
|---|---|
| ADO Repos | Update File |
| GitHub | Update File |
| GitLab | Update File |
| GitLab Org | Update File |
| Bitbucket | Update File |

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
| 1 | Navigate to Toolkits and open the ADO Repos toolkit instance. Open the Test Settings panel. | Test Settings panel opens. |
| 2 | From the tool dropdown, select 'Update File'. | Parameter fields load: File Path, Branch Name, File Query *, and optionally Commit Message. |
| 3 | Enter 'test/update-test.txt' in File Path and 'test-branch' in Branch Name. | Values are set. |
| 4 | Click inside the File Query * field. Type the 6-line OLD/NEW block pressing Enter between each line: 'OLD <<<<' [Enter] 'original text to replace' [Enter] '>>>> OLD' [Enter] 'NEW <<<<' [Enter] 'replacement text' [Enter] '>>>> NEW'. | All 6 lines appear in the field on separate rows. Pressing Enter does not navigate away or submit the form. |
| 5 | Click RUN TOOL. Wait for the response. | Response does NOT contain 'No OLD/NEW marker pairs found in file_query'. Response indicates the file was updated successfully. |
| 6 | Repeat steps 1–5 for each remaining toolkit type: GitHub, GitLab, GitLab Org, Bitbucket. | All 5 toolkit types accept multi-line input and return a successful update response without the marker error. |

## Expected Final State

All 5 toolkit types accept multi-line input and return a successful update response without the marker error.

## Pass/Fail Criteria

**Pass:**
- Multi-line File Query is accepted in Test Settings for all 5 toolkit types (ADO Repos, GitHub, GitLab, GitLab Org, Bitbucket)
- `update_file` executes and returns a success response without the marker error for all 5 toolkit types

**Fail:**
- Any toolkit type's File Query field collapses input or triggers navigation on Enter
- "No OLD/NEW marker pairs found in file_query..." error is returned for any toolkit type
