---
id: ELITEA-0426
title: "View/Edit from Chat: File in Folder Named Same as Bucket Opens Preview Without 400 Error [Parametrized]"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3874]
---
# ELITEA-0426: View/Edit from Chat: File in Folder Named Same as Bucket Opens Preview Without 400 Error [Parametrized]

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the View/Edit (eye) icon on a file chip in a Chat response, where the file path contains the bucket name as a folder segment, opens the Canvas preview successfully — without returning "Failed to fetch file: 400".

**Coverage (3 parametrized path patterns from bug #3874):**
- Pattern 1: `bucket → folder(=bucket_name) → file` — exact scenario from the bug report
- Pattern 2: `bucket → folder(=bucket_name) → any_folder → file` — bucket name in first position, deeper nesting
- Pattern 3: `bucket → any_folder → folder(=bucket_name) → file` — bucket name in non-root subfolder position

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- A Chat conversation is open with the Artifact Toolkit added as a participant, configured with bucket `preview-bucket`
- Bucket `preview-bucket` exists and is writable

## Test Data

Run once per row (create file via Chat prompt, then click View/Edit on the chip):

| # | Filename in prompt | Expected full object path | Description |
|---|---|---|---|
| 1 | `preview-bucket/c1-file.txt` | `preview-bucket/preview-bucket/c1-file.txt` | Folder name = bucket name (exact bug #3874 path) |
| 2 | `preview-bucket/sub/c2-file.txt` | `preview-bucket/preview-bucket/sub/c2-file.txt` | Bucket name in first folder, deeper nesting |
| 3 | `other-folder/preview-bucket/c3-file.txt` | `preview-bucket/other-folder/preview-bucket/c3-file.txt` | Bucket name in second-level folder |

File content for all rows: `Chat View/Edit parametrized test content.`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation that has the Artifact Toolkit attached as a participant with bucket `preview-bucket`. | Chat is open. Artifact Toolkit is visible in the Participants panel. |
| 2 | **Row 1 — Pattern: bucket_name/bucket_name/file** Send the prompt: 'Create a file named `preview-bucket/c1-file.txt` with content `Chat View/Edit parametrized test content.` in bucket `preview-bucket`'. | AI invokes createFile. Response confirms file created at `preview-bucket/preview-bucket/c1-file.txt`. A file chip for `c1-file.txt` appears in the chat response. |
| 3 | Click the View/Edit (eye) icon on the `c1-file.txt` chip in the chat response. | Canvas preview/edit modal opens as a full overlay. Content `Chat View/Edit parametrized test content.` is displayed. No "Failed to fetch file: 400" error. |
| 4 | Close the Canvas modal. **Row 2 — Pattern: bucket_name/bucket_name/any_folder/file** Send the prompt: 'Create a file named `preview-bucket/sub/c2-file.txt` with content `Chat View/Edit parametrized test content.` in bucket `preview-bucket`'. | AI creates the file. Response confirms path `preview-bucket/preview-bucket/sub/c2-file.txt`. A file chip for `c2-file.txt` appears. |
| 5 | Click the View/Edit (eye) icon on the `c2-file.txt` chip. | Canvas modal opens. Content displayed correctly. No "Failed to fetch file: 400" error. |
| 6 | Close the Canvas modal. **Row 3 — Pattern: any_folder/bucket_name/file** Send the prompt: 'Create a file named `other-folder/preview-bucket/c3-file.txt` with content `Chat View/Edit parametrized test content.` in bucket `preview-bucket`'. | AI creates the file. Response confirms path `preview-bucket/other-folder/preview-bucket/c3-file.txt`. A file chip for `c3-file.txt` appears. |
| 7 | Click the View/Edit (eye) icon on the `c3-file.txt` chip. | Canvas modal opens. Content displayed correctly. No "Failed to fetch file: 400" error. |

## Expected Final State

Canvas modal opens. Content displayed correctly. No "Failed to fetch file: 400" error.

## Pass/Fail Criteria

**Pass:**
- Canvas modal opens without error from Chat for ALL 3 path patterns
- File content is rendered correctly in the editor each time
- No "Failed to fetch file: 400" error for any pattern

**Fail:**
- "Failed to fetch file: 400" returned when clicking View/Edit eye icon from Chat for any of the 3 patterns
- Canvas modal blank or shows error state for any pattern
