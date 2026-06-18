---
id: ELITEA-0307
title: "Agent Execution Reads Image from Artifact – Claude Sonnet 4.6"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0307: Agent Execution Reads Image from Artifact – Claude Sonnet 4.6

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that an Agent configured with an Artifact Toolkit can successfully execute a readFile call on an image file using Claude Sonnet 4.6 without API-level errors.

**Coverage:**
- Agent with Artifact Toolkit completes readFile on an image using Claude Sonnet 4.6
- No 400 InternalSDKError with 'thinking' tag mismatch is raised
- Agent response includes image description in conversation output

## Preconditions

- Logged in to {{base_url}}
- An Agent exists (or can be created) with an Artifact Toolkit attached and readFile tool enabled
- The bucket associated with the toolkit contains at least one image file
- Claude Sonnet 4.6 is available as an LLM for the agent

## Test Data

- Agent name: any agent with Artifact Toolkit (readFile enabled)
- Bucket: bucket containing sample.png
- Image filename: sample.png
- LLM: Claude Sonnet 4.6

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from the sidebar. | Agents list page is displayed. |
| 2 | Open an existing agent or create a new one with the Artifact Toolkit added, readFile tool enabled. | Agent configuration is accessible. |
| 3 | Set the agent's LLM to Claude Sonnet 4.6. | Claude Sonnet 4.6 is selected. |
| 4 | Start a new conversation with the agent. | Chat interface opens with the agent active. |
| 5 | Send: 'Read the image sample.png from the artifact bucket and describe what you see.' | Agent invokes the readFile tool. |
| 6 | Observe the agent's response. | Agent returns an image description. No InternalSDKError with status 400 or 'thinking' tag message is present. |

## Expected Final State

Agent returns an image description. No InternalSDKError with status 400 or 'thinking' tag message is present.

## Pass/Fail Criteria

**Pass:**
- Agent reads the image successfully and returns a description
- No 400 API error is raised
- Execution completes within expected time

**Fail:**
- InternalSDKError status 400 with 'thinking' tag mismatch is raised
- Agent fails mid-execution or returns an error to the user
