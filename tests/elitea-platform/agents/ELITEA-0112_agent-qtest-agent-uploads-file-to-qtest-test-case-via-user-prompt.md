---
id: ELITEA-0112
title: "Agent → QTest: Agent Uploads File to QTest Test Case via User Prompt"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits, agent]
requirements: [3180]
---
# ELITEA-0112: Agent → QTest: Agent Uploads File to QTest Test Case via User Prompt

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an ELITEA Agent with the QTest toolkit connected can upload a file to a QTest test case via a natural language user prompt.

## Preconditions

- An ELITEA Agent is configured with QTest toolkit (including 'Add file to test case' tool) and Artifact Toolkit
- Artifact bucket contains a file at /my-bucket/test-file.png
- A valid QTest test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the configured ELITEA Agent and open a conversation | Agent conversation interface is open |
| 2 | Send the prompt: 'Upload the file /my-bucket/test-file.png to QTest test case [test_case_id] as an attachment' | Agent invokes 'Add file to test case' tool and reports success |
| 3 | Navigate to QTest and open the test case | test-file.png appears as an attachment on the QTest test case |

## Expected Final State

test-file.png appears as an attachment on the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
