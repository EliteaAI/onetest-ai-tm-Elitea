---
id: ELITEA-1129
title: "Artifact Toolkit Test Settings: create_file - Cleared Mutually Exclusive Field Not Included in Outgoing Request"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:artifacts, feat:toolkits, eng:frontend, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3632]
---
# ELITEA-1129: Artifact Toolkit Test Settings: create_file - Cleared Mutually Exclusive Field Not Included in Outgoing Request

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user fills one mutually exclusive field (filedata or filepath), clears it, and fills the other, the cleared field is absent from the outgoing request and the tool executes successfully without a mutually exclusive field validation error.


**Coverage:**
- filedata filled → cleared → filepath filled: cleared filedata is excluded from request
- filepath filled → cleared → filedata filled: cleared filepath is excluded from request
- Tool returns a success response with no mutually exclusive field validation error
- Outgoing request contains only the field that was last filled

## Preconditions

- Logged into ELITEA at {{base_url}}
- An Artifact Toolkit with create_file tool enabled is configured in the active project
- Toolkit detail page is open, Test Settings panel is visible on the right side
- A valid LLM model is selected in the Test Settings model dropdown
- A valid artifact bucket exists to receive the request
- Browser DevTools Network tab is open to inspect outgoing requests

## Test Data

- filename: test-file.txt
- filedata (Direction 1): hello world test content
- filepath (Direction 2): existing-reference-file.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any Artifact Toolkit detail page and navigate to the Test Settings panel | Test Settings panel is visible with the create_file tool selected and all fields empty |
| 2 | Fill in the 'filename' field with 'test-file.txt' | Filename field shows 'test-file.txt' |
| 3 | Fill in the 'filedata' field with 'hello world test content' | Filedata field shows the entered content |
| 4 | Clear the 'filedata' field completely (select all and delete) | Filedata field is now visually empty |
| 5 | Fill in the 'filepath' field with 'existing-reference-file.txt' | Filepath field shows the entered value |
| 6 | Click the Run/Test button to execute create_file | Request is sent; inspect Network tab for the outgoing payload |
| 7 | In DevTools Network tab, inspect the outgoing request payload for the create_file call | Payload contains 'filepath' and 'filename' but does NOT contain 'filedata' key at all |
| 8 | Verify the tool response in the Test Settings output area | Tool returns a success response; no mutually exclusive field validation error is shown |
| 9 | Reload the page to reset all fields, then fill 'filepath' with 'existing-reference-file.txt' | Filepath field shows the value |
| 10 | Clear the 'filepath' field completely | Filepath field is now visually empty |
| 11 | Fill in the 'filedata' field with 'hello world test content' | Filedata field shows the entered content |
| 12 | Click the Run/Test button to execute create_file | Request is sent; inspect Network tab |
| 13 | Inspect the outgoing request payload and verify the tool response | Payload contains 'filedata' and 'filename' but does NOT contain 'filepath' key; tool returns a success response |

## Expected Final State

Payload contains 'filedata' and 'filename' but does NOT contain 'filepath' key; tool returns a success response

## Pass/Fail Criteria

**Pass:**
- Cleared field is completely absent from the outgoing request payload in both directions
- Tool returns a success response in both directions
- No error message about mutually exclusive fields appears

**Fail:**
- Cleared field is present in the request as "" (empty string)
- Tool returns an error about mutually exclusive fields being set simultaneously
- Request fails with a validation error
