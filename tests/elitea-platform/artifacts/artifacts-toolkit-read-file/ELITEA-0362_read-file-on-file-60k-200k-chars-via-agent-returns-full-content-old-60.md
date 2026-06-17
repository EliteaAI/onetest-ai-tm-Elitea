---
id: ELITEA-0362
title: "read_file on file 60k–200k chars via Agent returns full content — old 60k limit no longer blocks"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0362: read_file on file 60k–200k chars via Agent returns full content — old 60k limit no longer blocks

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file between 60,000 and 200,000 characters, which was previously blocked by the old 60k limit, is now read fully by an Agent using the Artifact Toolkit.

**Coverage:**
- File in the 60k–200k range is returned in full with no size-limit error string
- The old error `[Content has N lines and exceeds size limit...]` no longer appears
- Agent response includes actual file content, not an error message

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- An Agent configured with an Artifact Toolkit pointing to a bucket containing test files
- Test file `medium_file.txt` (~80k chars) pre-uploaded to the bucket
- Chrome or Edge, latest stable

## Test Data

- File: `medium_file.txt` (~80,000 chars, above old 60k limit, below new 200k limit)
- Bucket: any bucket configured on the Artifact Toolkit
- Agent prompt: `"Read the full content of medium_file.txt"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page. Open the Agent configured with the Artifact Toolkit. | Agent chat or test panel opens. |
| 2 | Send prompt: "Read the full content of medium_file.txt" | Agent invokes the read_file tool. |
| 3 | Inspect the Agent response. | Response contains actual file content — no error string `[Content has N lines and exceeds size limit...]` appears. Full ~80k content is visible. |

## Expected Final State

Response contains actual file content — no error string `[Content has N lines and exceeds size limit...]` appears. Full ~80k content is visible.

## Pass/Fail Criteria

**Pass:**
- Full file content returned without any size-limit error string
- Content length matches the actual file (~80k chars)

**Fail:**
- Response contains `[Content has N lines and exceeds size limit. Use partial read options.]`
- Response is empty or truncated unexpectedly
