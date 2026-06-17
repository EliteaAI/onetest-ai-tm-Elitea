---
id: ELITEA-0304
title: "Agent Execution Reads Image from Artifact – Claude Sonnet 4.5"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0304: Agent Execution Reads Image from Artifact – Claude Sonnet 4.5

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an Agent configured with an Artifact Toolkit can successfully execute a readFile call on an image file using Claude Sonnet 4.5 without a litellm base64 parsing error.

**Coverage:**
- Agent with Artifact Toolkit completes readFile on an image using Claude Sonnet 4.5
- No 500 litellm APIConnectionError is raised
- Agent response includes image description in conversation output

## Preconditions

- Logged in to {{base_url}}
- An Agent exists (or can be created) with an Artifact Toolkit attached and readFile tool enabled
- The bucket associated with the toolkit contains at least one image file
- Claude Sonnet 4.5 is available as an LLM for the agent

## Test Data

- Agent name: any agent with Artifact Toolkit (readFile enabled)
- Bucket: bucket containing sample.png
- Image filename: sample.png
- LLM: Claude Sonnet 4.5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from the sidebar. | Agents list page is displayed. |
| 2 | Open an existing agent or create a new one with the Artifact Toolkit added, readFile tool enabled. | Agent configuration is accessible. |
| 3 | Set the agent's LLM to Claude Sonnet 4.5. | Claude Sonnet 4.5 is selected. |
| 4 | Start a new conversation with the agent. | Chat interface opens with the agent active. |
| 5 | Send: 'Read the image sample.png from the artifact bucket and describe what you see.' | Agent invokes the readFile tool. |
| 6 | Observe the agent's response. | Agent returns an image description. No 500 error, no litellm base64 parsing error, no 'too many values to unpack' error is present. |

## Expected Final State

Agent returns an image description. No 500 error, no litellm base64 parsing error, no 'too many values to unpack' error is present.

## Pass/Fail Criteria

**Pass:**
- Agent reads the image successfully and returns a description
- No 500 API error is raised
- Execution completes without litellm errors

**Fail:**
- InternalSDKError status 500 with litellm APIConnectionError is raised
- _parse_base64_image fails with ValueError
- Agent fails mid-execution or returns an error to the user
