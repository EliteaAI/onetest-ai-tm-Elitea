---
id: ELITEA-4106
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Agent Integration with Image Content"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4106: ADO Toolkit — Agent Integration with Image Content

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that agents receive extracted image descriptions in tool response and can use them in generated outputs.

## Preconditions

- Agent configured to use ADO toolkit with `process_images: true`
- ADO work item has comments with images
- Agent chat interface available
- LLM vision model successfully extracting image content

## Test Data

| Scenario | Action | Expected |
|----------|--------|----------|
| Agent queries comments | Agent calls get_comments | Image descriptions in response |
| Agent references image | Agent generates response | Image content referenced |
| Chat display | User views agent output | Image descriptions visible |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Start agent conversation; ask agent to analyze ADO work item comments. | Agent calls get_comments tool. |
| 2 | Verify agent receives image descriptions in tool response. | Response includes image content alongside text. |
| 3 | Verify agent can reference and use image content in response. | Agent mentions image details in generated text. |
| 4 | Verify agent reasoning incorporates image context. | Agent's analysis includes insights from images. |
| 5 | Query agent about specific image content (e.g., "What does the screenshot show?"). | Agent provides accurate description based on extracted content. |
| 6 | Verify image descriptions appear contextually in chat output. | Images referenced naturally in conversation. |
| 7 | Test multi-turn conversation: agent maintains image context across turns. | Image content remains accessible in follow-up questions. |
| 8 | Test agent with pipeline: verify image content flows through pipeline steps. | Each step receives image descriptions from prior tool calls. |

## Expected Final State

- Agent receives image descriptions in tool response
- Agent can reference and use image content
- Agent reasoning incorporates image context
- Image descriptions appear contextually in chat output
- Multi-turn conversations maintain image context
- Pipelines process image content correctly

## Pass/Fail Criteria

**Pass:** Agent receives/uses image content; context incorporated; chat display accurate; pipelines work.  
**Fail:** Agent doesn't receive image descriptions; content not used; context lost; pipeline failures.
