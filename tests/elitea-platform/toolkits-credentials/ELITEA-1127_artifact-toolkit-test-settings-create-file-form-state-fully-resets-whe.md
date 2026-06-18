---
id: ELITEA-1127
title: "Artifact Toolkit Test Settings: create_file - Form State Fully Resets When Switching Tools"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:artifacts, feat:toolkits, eng:frontend, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3632]
---
# ELITEA-1127: Artifact Toolkit Test Settings: create_file - Form State Fully Resets When Switching Tools

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that switching between tools in the Artifact Toolkit Test Settings panel fully resets the create_file form state — no previously entered or cleared values are retained or carried into a subsequent tool's request.

**Coverage:**
- Switching away from create_file after filling/clearing fields clears all entered values
- Switching back to create_file shows a clean/empty form
- Executing a different tool after switching does not include any create_file fields in its request
- Form state isolation between tools is maintained

## Preconditions

- Logged into ELITEA at {{base_url}}
- Artifact Toolkit with at least create_file and one other tool (e.g., read_file) enabled
- Test Settings panel open, LLM model selected
- Browser DevTools Network tab open

## Test Data

- filename: state-test.txt
- filedata: state test value
- filepath: state-ref-path.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any valid Artifact toolkit | The Artifact toolkit page opens successfully. |
| 2 | Select create_file in the Test Settings tool selector | create_file form fields are displayed and empty |
| 3 | Fill 'filename' with 'state-test.txt', 'filedata' with 'state test value', and 'filepath' with 'state-ref-path.txt' | All three fields show their entered values |
| 4 | Clear the 'filedata' field completely | Filedata field is visually empty |
| 5 | Switch to a different tool (e.g., read_file) in the tool selector | read_file form fields are displayed |
| 6 | Switch back to create_file in the tool selector | create_file form is displayed with all fields empty — no previously entered or cleared values retained |
| 7 | Switch to read_file again and fill in its required fields | read_file fields accept input |
| 8 | Click Run/Test for read_file and inspect the outgoing request payload in DevTools | Payload contains only read_file fields; no create_file fields (filename, filedata, filepath) are present |
| 9 | Verify the read_file tool response | read_file returns a success response; no create_file validation errors appear |
| 10 | Switch back to create_file and confirm fields are still empty | All create_file fields remain empty; no state contamination from any previous interaction |

## Expected Final State

All create_file fields remain empty; no state contamination from any previous interaction

## Pass/Fail Criteria

**Pass:**
- All create_file form fields are empty after switching tools and switching back
- read_file request payload contains no create_file fields
- Tools execute independently with no cross-contamination of form state

**Fail:**
- Previously entered or cleared values from create_file are still visible after switching tools and back
- read_file request includes create_file fields
- Any tool request is contaminated with field values from a previously selected tool
