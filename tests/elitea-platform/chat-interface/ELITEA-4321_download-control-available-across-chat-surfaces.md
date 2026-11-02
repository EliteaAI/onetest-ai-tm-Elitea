---
id: ELITEA-4321
title: "Download Control Available Consistently Across Direct Chat, Agent-Participant, and Pipeline-Participant Surfaces"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- User has an existing published Agent that can be added as a chat participant
- User has an existing Pipeline that can be added as a chat participant and produces a code-block response

## Test Data

| Surface | Setup |
|---|---|
| Direct chat | No participant added; default LLM response |
| Agent-as-participant | Agent added as the sole chat participant |
| Pipeline-as-participant | Pipeline added as the sole chat participant |
| Prompt (all surfaces) | "Give me a short json config example" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a direct chat (no participant) and send the Test Data prompt | AI responds with a message containing a fenced json code block, with Edit code/Copy code/Download in its toolbar |
| 2 | Click the Download icon on the direct chat response | File downloads successfully with content matching the code block |
| 3 | Start a new conversation, add the Agent as the sole participant, and send the same prompt | Agent responds with a message containing a fenced json code block, with the same toolbar including Download |
| 4 | Click the Download icon on the Agent-participant response | File downloads successfully with content matching the code block |
| 5 | Start a new conversation, add the Pipeline as the sole participant, and trigger it with the same prompt (or its equivalent pipeline input) | Pipeline response renders a message containing a fenced json code block, with the same toolbar including Download |
| 6 | Click the Download icon on the Pipeline-participant response | File downloads successfully with content matching the code block |

## Expected Final State

The Download control is present, visually consistent, and functionally correct for code blocks rendered in direct chat, Agent-as-participant, and Pipeline-as-participant conversations alike.

## Pass/Fail Criteria

**Pass:**
- Download icon appears in the code block toolbar on all three chat surfaces (direct, Agent-participant, Pipeline-participant)
- Clicking Download produces a correct, matching file on all three surfaces

**Fail:**
- Download icon is missing, disabled, or non-functional on any one of the three chat surfaces
- Downloaded file content differs from the displayed code block on any surface
