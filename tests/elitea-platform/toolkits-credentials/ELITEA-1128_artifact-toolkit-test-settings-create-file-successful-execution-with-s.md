---
id: ELITEA-1128
title: "Artifact Toolkit Test Settings: create_file - Successful Execution with Single Mutually Exclusive Field"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:artifacts, feat:toolkits, eng:frontend, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3632]
---
# ELITEA-1128: Artifact Toolkit Test Settings: create_file - Successful Execution with Single Mutually Exclusive Field

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that create_file executes successfully when only one of filedata or filepath is provided without any prior clearing of the other field — confirming no regression on the clean-state workflow after the fix.


**Coverage:**
- filedata provided alone (no prior interaction with filepath): tool executes successfully
- filepath provided alone (no prior interaction with filedata): tool executes successfully
- No regression introduced by the fix on the standard happy-path flow

## Preconditions

- Logged into ELITEA at {{base_url}}
- An Artifact Toolkit with create_file tool enabled is configured in the active project
- Test Settings panel is open, LLM model is selected
- A valid artifact bucket exists

## Test Data

- filename (Scenario A): baseline-filedata-test.txt
- filedata: baseline content line one
- filename (Scenario B): baseline-filepath-test.txt
- filepath: source-reference.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any Artifact Toolkit detail page, navigate to Test Settings panel with create_file selected | All form fields are empty and clean |
| 2 | Fill 'filename' with 'baseline-filedata-test.txt' and 'filedata' with 'baseline content line one'; leave 'filepath' untouched | Only filename and filedata fields contain values; filepath remains empty |
| 3 | Open DevTools Network tab, then click Run/Test | Request is sent |
| 4 | Inspect the outgoing request payload | Payload contains 'filename' and 'filedata' only; 'filepath' is absent |
| 5 | Verify the tool response in the output area | Tool returns a success response; no validation error |
| 6 | Reload the page to reset all fields | All fields are empty |
| 7 | Fill 'filename' with 'baseline-filepath-test.txt' and 'filepath' with 'source-reference.txt'; leave 'filedata' untouched | Only filename and filepath fields contain values; filedata remains empty |
| 8 | Click Run/Test and inspect the outgoing request payload | Payload contains 'filename' and 'filepath' only; 'filedata' is absent |
| 9 | Verify the tool response | Tool returns a success response; no validation error |

## Expected Final State

Tool returns a success response; no validation error

## Pass/Fail Criteria

**Pass:**
- Both scenarios return success responses with no validation errors
- Request payloads contain only the fields that were filled
- No regression in the standard single-field workflow

**Fail:**
- Either scenario returns a mutually exclusive fields error
- Request payload unexpectedly includes both fields
- Tool fails to execute when only one mutually exclusive field is provided
