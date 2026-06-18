---
id: ELITEA-0286
title: "edit_file Reports Per-Edit Status When Multiple Edits Are Submitted and Some Fail"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3574]
---
# ELITEA-0286: edit_file Reports Per-Edit Status When Multiple Edits Are Submitted and Some Fail

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that when `edit_file` is called with multiple edit operations simultaneously and some fail due to non-matching search strings, the tool output explicitly identifies which edits succeeded and which failed — rather than returning a generic aggregate message.

**Coverage:**
- `edit_file` called with 3 replacement blocks (1 valid, 2 invalid search strings)
- Tool output lists per-edit status: 1 succeeded, 2 failed with detail on which blocks were not found
- File is partially modified — only the valid edit is applied
- Generic aggregate-only messages (e.g. "Successfully applied 1 edit(s)" with no breakdown) are treated as failures
- Feedback is sufficient for an agent to identify and retry only the failed edits

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Artifacts Toolkit is configured and available in the project
- A file `multi_edit_test.txt` exists in a bucket (e.g. `test-bucket`) with content: "Hello World! I am Spider Man. Peter Parker is friendly."
- Navigate to the Artifacts Toolkit page → open Test Settings

## Test Data

- Bucket name: `test-bucket` (any bucket containing the file)
- File name: `multi_edit_test.txt`
- File initial content: "Hello World! I am Spider Man. Peter Parker is friendly."
- Tool: `edit_file`
- Edit block 1 (valid): search="Peter Parker" → replace="Tony Stark"
- Edit block 2 (invalid): search="Bruce Banner" → replace="Hulk"
- Edit block 3 (invalid): search="Steve Rogers" → replace="Captain America"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifacts Toolkit page and open the Test Settings tab. | Test Settings panel is displayed with a list of available toolkit tools. |
| 2 | Select the `edit_file` tool from the tool list. | The `edit_file` tool input form is displayed with its required parameters. |
| 3 | Fill in the parameters: file name = `multi_edit_test.txt`, bucket = `test-bucket`. Add 3 replacement blocks: (1) search="Peter Parker" → replace="Tony Stark", (2) search="Bruce Banner" → replace="Hulk", (3) search="Steve Rogers" → replace="Captain America". | All three replacement blocks are populated in the tool parameter form. |
| 4 | Click Run to execute the `edit_file` tool. | The tool executes and the raw output is displayed in the Test Settings response area. |
| 5 | Inspect the full tool output in the response panel. | Output includes a per-edit breakdown: block 1 succeeded ("Peter Parker" found and replaced), blocks 2 and 3 failed with the unmatched search strings explicitly identified. A generic message without breakdown (e.g. only "Successfully applied 1 edit(s)") is NOT acceptable. |
| 6 | Navigate to Artifacts, open bucket `test-bucket`, and read `multi_edit_test.txt`. | File content shows "Tony Stark" in place of "Peter Parker". The rest of the content is unchanged — only the 1 valid edit was applied. |

## Expected Final State

File content shows "Tony Stark" in place of "Peter Parker". The rest of the content is unchanged — only the 1 valid edit was applied.

## Pass/Fail Criteria

**Pass:**
- Tool output explicitly lists status per edit (e.g. "Applied 1 edit. Failed to apply 2 edits. Matches not found for: ['Bruce Banner', 'Steve Rogers']")
- File is updated only where the match succeeded
- Failed search strings are identifiable from the tool output

**Fail:**
- Tool returns only a generic message (e.g. "Successfully applied 1 edit(s)") without per-edit breakdown
- File is incorrectly not modified (valid edit not applied) or incorrectly modified (invalid edits applied)
- No information is provided to distinguish which edits passed and which failed
