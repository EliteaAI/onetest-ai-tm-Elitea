---
id: ELITEA-0354
title: "File uploaded via Artifacts page (80k chars) then read by Agent — full content returned"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0354: File uploaded via Artifacts page (80k chars) then read by Agent — full content returned

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify the end-to-end flow: upload a file via the Artifacts Application page, then have an Agent read it — file previously blocked at 60k now returns fully.

**Coverage:**
- File upload works correctly via Artifacts page UI
- Agent reads the newly uploaded file at ~80k chars (above old 60k limit, within new 200k limit)
- Full content returned — upload path and read path are independent

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Artifacts page accessible from the sidebar
- Agent configured with Artifact Toolkit pointing to the same bucket
- Local file `medium_file.txt` (~80k chars) prepared for upload

## Test Data

- File to upload: `medium_file.txt` (~80,000 chars)
- Target bucket: the bucket configured on the Agent's Artifact Toolkit
- Agent prompt: `"Read the full content of medium_file.txt"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifacts page from the sidebar. Open the target bucket. | Bucket file list is displayed. |
| 2 | Upload `medium_file.txt` (~80k chars) to the bucket. | Upload completes. File appears in the bucket file list with correct name and size. |
| 3 | Navigate to Agents page. Open the Agent with the Artifact Toolkit pointing to the same bucket. | Agent opens. |
| 4 | Send prompt: "Read the full content of medium_file.txt" | Agent invokes read_file. |
| 5 | Inspect the Agent response. | Full ~80k content returned. No size-limit error string. |

## Expected Final State

Full ~80k content returned. No size-limit error string.

## Pass/Fail Criteria

**Pass:**
- File uploads successfully via Artifacts page
- Agent reads the file fully — no size-limit error
- Content matches the uploaded file

**Fail:**
- Upload fails
- Agent returns size-limit error for the ~80k file
- Returned content is truncated
