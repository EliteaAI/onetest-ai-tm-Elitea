---
id: ELITEA-0364
title: "read_file on file >200k chars via Agent returns size-limit error — 200k cap enforced on agent path"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0364: read_file on file >200k chars via Agent returns size-limit error — 200k cap enforced on agent path

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Agent path enforces the 200k character limit — a file exceeding 200,000 chars returns the size-limit error string, not the full content.

**Coverage:**
- Agent path uses `skip_size_check=False` by default
- File >200k triggers the error string `[Content has N lines and exceeds size limit...]`
- Agent correctly surfaces the error to the user so they can use partial read options

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Agent configured with Artifact Toolkit
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the bucket

## Test Data

- File: `xlarge_file.txt` (~300,000 chars, above the 200k limit)
- Agent prompt: `"Read the full content of xlarge_file.txt"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page. Open the Agent configured with the Artifact Toolkit. | Agent chat or test panel opens. |
| 2 | Send prompt: "Read the full content of xlarge_file.txt" | Agent invokes the read_file tool. |
| 3 | Inspect the Agent response. | Response contains the size-limit error string: `[Content has N lines and exceeds size limit. Use partial read options.]` — full content is NOT returned. |

## Expected Final State

Response contains the size-limit error string: `[Content has N lines and exceeds size limit. Use partial read options.]` — full content is NOT returned.

## Pass/Fail Criteria

**Pass:**
- Size-limit error string returned for file >200k chars
- Agent does not return raw file content unexpectedly large

**Fail:**
- Full 300k content returned (limit not enforced on agent path)
- Response is a generic error unrelated to size
