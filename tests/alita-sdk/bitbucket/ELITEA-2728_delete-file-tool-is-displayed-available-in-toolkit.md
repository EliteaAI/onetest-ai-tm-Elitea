---
id: ELITEA-2728
title: "BitBucket - delete_file: Tool is displayed/available in the toolkit"
priority: critical
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2728: BitBucket - delete_file: Tool is displayed/available in the toolkit

**Module:** Bitbucket · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the new `delete_file` tool is visible/selectable in the BitBucket toolkit's tool list, reported by `get_available_tools()`, and has all required parameters documented.

## Preconditions

BitBucket toolkit is configured against a Git repository.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the BitBucket toolkit configuration/tool selection UI | `delete_file` (or its display name) appears in the list alongside existing BitBucket tools (create_file, read_file, update_file, list_files) |
| 2 | Call `get_available_tools()` on the toolkit | `delete_file` is present in the returned list with name and description |
| 3 | Check the tool documentation/schema | All required parameters are documented: `file_path` (required, string), `branch_name` (required, string), `commit_message` (optional, string) |
| 4 | Verify parameter descriptions | Parameter descriptions are clear and indicate which are required vs. optional |

## Expected Final State

`delete_file` is listed as an available tool in both the UI and `get_available_tools()` with complete parameter documentation.

## Pass/Fail Criteria

**Pass:**
- delete_file is listed in the toolkit configuration UI
- delete_file is present in get_available_tools()
- All parameters (file_path, branch_name, commit_message) are documented with correct types and required/optional flags

**Fail:**
- delete_file is missing from either location
- Parameter documentation is incomplete or incorrect
