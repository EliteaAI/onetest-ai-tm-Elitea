---
id: ELITEA-0905
title: "Unsupported File Type Rejected With Clear Error"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0905: Unsupported File Type Rejected With Clear Error

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching a file with an unsupported extension is handled correctly — ignored when using the file browser, and rejected with a clear error banner when dragged and dropped.

**Coverage:**
- File browser (paperclip): .exe file is ignored/not selectable — no error shown, file simply does not appear
- Drag and drop: .exe file triggers "Invalid file types detected" error banner listing allowed extensions
- File not stored in attachments bucket in either case

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

- Unsupported file: software.exe (.exe extension)
- Entry point 1: file browser via paperclip — file ignored
- Entry point 2: drag and drop — error banner shown

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Click the paperclip icon to open the file browser. | File browser opens. |
| 2 | Attempt to select an .exe file (e.g., software.exe) from the file browser. | The .exe file is ignored — it is either not selectable or does not appear as an attachment in the chat input. No error message is shown. |
| 3 | Drag and drop the .exe file (e.g., software.exe) directly onto the chat input area. | An error banner appears: 'Invalid file types detected: CW_OS.exe (.exe). Only [list of allowed extensions] files are allowed.' The file does not appear as an attachment in the input. |
| 4 | Navigate to Artifacts → attachments bucket. | software.exe is NOT present in the bucket in either case. |

## Expected Final State

software.exe is NOT present in the bucket in either case.

## Pass/Fail Criteria

**Pass:**
- .exe not selectable or ignored via file browser with no error
- Drag and drop of .exe triggers "Invalid file types detected" error banner
- File not stored in attachments bucket in either case

**Fail:**
- .exe accepted via file browser
- Drag and drop shows no error or a generic error
- File stored in bucket after rejection
