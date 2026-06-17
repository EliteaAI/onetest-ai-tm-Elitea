---
id: ELITEA-1081
title: "GitLab - Agent Processes get_issue Comments End-to-End in Chat"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [r-2.0.2]
requirements: [EliteaAI/elitea_issues#4055]
---
# ELITEA-1081: GitLab - Agent Processes get_issue Comments End-to-End in Chat

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that an ELITEA agent configured with the GitLab toolkit can call `get_issue`, receive structured comments, and meaningfully process them — listing comment authors or summarizing bodies — confirming the fix is functional in the full integration path.

**Coverage:**
- Agent invokes `get_issue` successfully from Chat
- Structured comments array is passed to agent LLM context
- Agent can extract and present individual comment fields (`body`, `user`)
- No raw string dump or parsing error in the agent response

## Preconditions

- Logged into {{base_url}} (stage environment)
- Agent configured with GitLab toolkit (get_issue tool enabled, instructions: "Help user retrieve and analyze GitLab issues")
- Test issue EliteaAI/elitea_issues#1 exists with at least 2 comments
- New chat conversation open with the agent added as participant

## Test Data

- Chat prompt 1: "Get issue EliteaAI/elitea_issues#1 from the repository and list all comment authors"
- Chat prompt 2: "Summarize all comments from issue EliteaAI/elitea_issues#1"
- Expected: agent lists the actual commenter usernames (e.g., project_2372_bot_...)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open ELITEA Chat, add the GitLab-toolkit agent as participant | Agent added, chat ready |
| 2 | Send: 'Get issue EliteaAI/elitea_issues#1 from the repository and list all comment authors' | Agent invokes `get_issue` tool (chipset visible in chat) |
| 3 | Verify agent response lists comment authors — at least one username is shown | Response contains ≥1 GitLab username matching actual commenters, not a raw Python list string |
| 4 | Send: 'Summarize all comments from issue EliteaAI/elitea_issues#1' | Agent processes comments array and begins composing a summary |
| 5 | Verify agent response contains a meaningful summary of comment bodies | Summary is coherent and references actual comment text — not "[{'body': '...'}]" verbatim |
| 6 | Verify no error message or fallback response is shown in either reply | Agent completes both requests without error or empty response |

## Expected Final State

Agent completes both requests without error or empty response

## Pass/Fail Criteria

**Pass:**
- Agent successfully invokes `get_issue` and returns structured results
- Comment authors and/or comment bodies are correctly extracted and presented
- No raw Python list string appears in the agent's response

**Fail:**
- Agent responds with "I couldn't parse the comments" or similar error
- Agent output contains the raw stringified list (old broken behavior)
- Tool invocation fails with a validation or type error
