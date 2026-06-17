---
id: ELITEA-0111
title: "Agent → SharePoint: Agent Uploads File to SharePoint via User Prompt"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits, agent]
requirements: [3180]
---
# ELITEA-0111: Agent → SharePoint: Agent Uploads File to SharePoint via User Prompt

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an ELITEA Agent with the SharePoint toolkit connected can upload a file to SharePoint via a natural language user prompt.

## Preconditions

- An ELITEA Agent is configured with SharePoint toolkit (including 'Upload file' tool) and Artifact Toolkit
- Artifact bucket contains a file at /my-bucket/test-file.png
- A valid SharePoint site and document library are available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the configured ELITEA Agent and open a conversation | Agent conversation interface is open |
| 2 | Send the prompt: 'Upload the file /my-bucket/test-file.png to the SharePoint document library' | Agent invokes 'Upload file' tool and reports success |
| 3 | Navigate to the SharePoint document library | test-file.png appears in the SharePoint document library |

## Expected Final State

test-file.png appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
