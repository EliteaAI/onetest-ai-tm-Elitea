---
id: ELITEA-0360
title: "read_file on file >200k chars via Pipeline LLM Node (Agent with Artifact Toolkit) returns full content"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0360: read_file on file >200k chars via Pipeline LLM Node (Agent with Artifact Toolkit) returns full content

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when an LLM Node in a Pipeline uses an Agent configured with the Artifact Toolkit to read a large file, the file content is returned in full with no size-limit constraint.

**Coverage:**
- Pipeline LLM Node → Agent with Artifact Toolkit path does not enforce 200k limit
- Full content of >200k file flows through to the LLM node output
- No size-limit error string in run details

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A Pipeline with an LLM Node configured to use an Agent that has the Artifact Toolkit
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the bucket
- Agent prompt instructs it to read the large file

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Pipeline: LLM Node with Agent (Artifact Toolkit), task prompt: `"Read xlarge_file.txt and summarize"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline with the LLM Node. Confirm the Agent has Artifact Toolkit configured and the task prompt references `xlarge_file.txt`. | Pipeline and Agent configuration confirmed. |
| 2 | Run the pipeline. | Pipeline execution starts. LLM Node invokes the Agent. |
| 3 | Inspect Run Details for the LLM Node — check the tool call response for read_file. | read_file tool call returns full file content (~300k chars) without size-limit error. Agent is able to process the content. |

## Expected Final State

read_file tool call returns full file content (~300k chars) without size-limit error. Agent is able to process the content.

## Pass/Fail Criteria

**Pass:**
- read_file returns full content to the LLM Node with no size-limit error
- Pipeline run completes without failure caused by file size

**Fail:**
- Size-limit error string in tool call response inside LLM Node
- Pipeline fails due to content size
