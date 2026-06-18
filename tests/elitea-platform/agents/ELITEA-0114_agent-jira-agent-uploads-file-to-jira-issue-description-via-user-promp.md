---
id: ELITEA-0114
title: "Agent → Jira: Agent Uploads File to Jira Issue Description via User Prompt"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits, agent]
requirements: [3180]
---
# ELITEA-0114: Agent → Jira: Agent Uploads File to Jira Issue Description via User Prompt

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an ELITEA Agent with the Jira toolkit connected can upload a file to a Jira issue description via a natural language user prompt.

## Preconditions

- An ELITEA Agent is configured with Jira toolkit (including 'Add file to issue description' tool) and Artifact Toolkit
- Artifact bucket contains a file at /my-bucket/test-file.png
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the configured ELITEA Agent and open a conversation | Agent conversation interface is open |
| 2 | Send the prompt: 'Upload the file /my-bucket/test-file.png to the description of Jira issue [issue_key]' | Agent invokes 'Add file to issue description' tool and reports success |
| 3 | Navigate to Jira and open the issue | test-file.png reference appears in the description of the Jira issue |

## Expected Final State

test-file.png reference appears in the description of the Jira issue

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
