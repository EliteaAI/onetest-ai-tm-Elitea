---
id: ELITEA-0115
title: "Agent → TestRail: Agent Uploads File to TestRail Test Case via User Prompt"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits, agent]
requirements: [3180]
---
# ELITEA-0115: Agent → TestRail: Agent Uploads File to TestRail Test Case via User Prompt

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an ELITEA Agent with the TestRail toolkit connected can upload a file to a TestRail test case via a natural language user prompt.

## Preconditions

- An ELITEA Agent is configured with TestRail toolkit (including 'Add file to case' tool) and Artifact Toolkit
- Artifact bucket contains a file at /my-bucket/test-file.png
- A valid TestRail test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the configured ELITEA Agent and open a conversation | Agent conversation interface is open |
| 2 | Send the prompt: 'Upload the file /my-bucket/test-file.png to TestRail test case [case_id] as an attachment' | Agent invokes 'Add file to case' tool and reports success |
| 3 | Navigate to TestRail and open the test case | test-file.png appears as an attachment on the TestRail test case |

## Expected Final State

test-file.png appears as an attachment on the TestRail test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
