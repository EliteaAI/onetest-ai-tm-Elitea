---
id: ELITEA-0113
title: "Agent → Confluence: Agent Uploads File to Confluence Page via User Prompt"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits, agent]
requirements: [3180]
---
# ELITEA-0113: Agent → Confluence: Agent Uploads File to Confluence Page via User Prompt

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an ELITEA Agent with the Confluence toolkit connected can upload a file to a Confluence page via a natural language user prompt.

## Preconditions

- An ELITEA Agent is configured with Confluence toolkit (including 'Add file to page' tool) and Artifact Toolkit
- Artifact bucket contains a file at /my-bucket/test-file.png
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the configured ELITEA Agent and open a conversation | Agent conversation interface is open |
| 2 | Send the prompt: 'Upload the file /my-bucket/test-file.png to Confluence page [page_id]' | Agent invokes 'Add file to page' tool and reports success |
| 3 | Navigate to Confluence and open the page | test-file.png appears on the Confluence page |

## Expected Final State

test-file.png appears on the Confluence page

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
