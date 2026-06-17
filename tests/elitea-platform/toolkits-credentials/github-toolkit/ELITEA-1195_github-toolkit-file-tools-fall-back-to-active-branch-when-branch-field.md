---
id: ELITEA-1195
title: "GitHub Toolkit — File Tools Fall Back to Active Branch When Branch Field Is Empty"
priority: high
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, int:github, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5031]
---
# ELITEA-1195: GitHub Toolkit — File Tools Fall Back to Active Branch When Branch Field Is Empty

**Module:** Github Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that `read_multiple_files` and `grep_file` in the GitHub toolkit fall back to the configured Active Branch when the optional Branch field is left empty, instead of passing `None` as the branch value.

**Coverage:**
- Empty Branch field fallback behavior for `read_multiple_files`
- Empty Branch field fallback behavior for `grep_file`
- Active Branch is used as fallback when Branch field is blank
- No `None` branch error appears in the tool response

## Preconditions

- User is logged in to {{base_url}}
- A GitHub Toolkit exists with Active Branch configured (e.g., `main`)
- At least one readable file exists on that branch (e.g., `README.md`)
- User has permission to open Test Settings for the toolkit tools

## Test Data

| Variable | Value |
|---|---|
| Active Branch | `main` |
| File path | `README.md` (valid file on the Active Branch) |
| Search pattern (for `grep_file`) | `README` |
| Branch field | (empty — no value entered) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the GitHub Toolkit and confirm its Active Branch is set to `main`. | Toolkit configuration shows Active Branch = `main`. |
| 2 | Navigate to Test Settings for the Read multiple files tool. | Test Settings panel opens for `read_multiple_files`. |
| 3 | Enter `README.md` in the file path field. Leave the Branch field empty. | File path is populated; Branch field remains blank. |
| 4 | Click RUN TOOL. | Tool executes without error. File content of `README.md` is returned. The response does NOT contain `"branch None"` or any `None`-related error. |
| 5 | Navigate to Test Settings for the Grep file tool. | Test Settings panel opens for `grep_file`. |
| 6 | Enter `README.md` as the file path and `README` as the search pattern. Leave the Branch field empty. | Inputs are populated; Branch field remains blank. |
| 7 | Click RUN TOOL. | Tool executes without error. Matching lines from the file are returned. The response does NOT contain `"branch None"` or any `None`-related error. |

## Expected Final State

Tool executes without error. Matching lines from the file are returned. The response does NOT contain `"branch None"` or any `None`-related error.

## Pass/Fail Criteria

**Pass:**
- Both tools execute successfully with an empty Branch field
- File content / grep results are returned for the Active Branch (`main`)
- No `"branch None"` string appears in any response
- Active Branch is transparently used as the fallback value

**Fail:**
- Either tool returns `"Error reading file: ... on branch None after 3 attempts"`
- `None` appears in a branch-related error message in any response
- Tool returns empty content when the file clearly exists on the Active Branch
