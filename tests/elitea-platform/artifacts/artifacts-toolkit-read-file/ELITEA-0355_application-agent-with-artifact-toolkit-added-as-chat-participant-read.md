---
id: ELITEA-0355
title: "Application (Agent with Artifact Toolkit) added as Chat participant reads file 60k–200k — full content returned"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0355: Application (Agent with Artifact Toolkit) added as Chat participant reads file 60k–200k — full content returned

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Application (published Agent with Artifact Toolkit) is used as a Chat participant to read a file in the 60k–200k range, the full content is returned — the agent path 200k limit applies and the file is within it.

**Coverage:**
- Application added as Chat participant invokes read_file via agent path
- File ~80k (above old limit, within new 200k limit) returned fully
- Same agent-path 200k limit applies regardless of Chat or direct Agent context

## Preconditions

- Logged in to {{base_url}}
- A published Application (Agent with Artifact Toolkit) exists in the project
- File `medium_file.txt` (~80k chars) pre-uploaded to the toolkit bucket
- Chrome or Edge, latest stable

## Test Data

- File: `medium_file.txt` (~80,000 chars)
- Chat message: `"Read the full content of medium_file.txt"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Start a new conversation. Add the Application (Agent with Artifact Toolkit) as a participant. | Conversation started with the application participant active. |
| 2 | Send message: "Read the full content of medium_file.txt" | Application invokes read_file tool. |
| 3 | Inspect the chat response. | Full ~80k content returned in chat. No size-limit error string appears. |

## Expected Final State

Full ~80k content returned in chat. No size-limit error string appears.

## Pass/Fail Criteria

**Pass:**
- Full file content returned in Chat response
- No size-limit error for ~80k file on agent path

**Fail:**
- Size-limit error returned (old 60k limit regression)
- Response truncated or empty
