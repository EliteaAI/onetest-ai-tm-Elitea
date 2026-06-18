---
id: ELITEA-1012
title: "Sensitive Tool Intercepted in Chat with Agent Participant"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1012: Sensitive Tool Intercepted in Chat with Agent Participant

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the authorization guardrail middleware intercepts sensitive tool execution when the agent is added as a participant in a Chat conversation (not the Agent page).

## Preconditions

- github > create_pull_request configured as sensitive
- A Chat conversation is open with the GitHub-toolkit agent added as a participant

## Test Data

- Chat prompt: "Please create a pull request from 'feature/chat-branch' to 'main' in repo 'elitea/backend-api'"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation. Add the GitHub toolkit agent as a participant. | Agent is listed as participant. |
| 2 | Send the prompt requesting PR creation: 'Please create a pull request from feature/chat-branch to main in repo elitea/backend-api'. | Agent begins processing in chat. |
| 3 | Observe the chat area. | Authorization dialog appears in the chat before tool execution. |
| 4 | Verify the dialog shows the correct action name and parameters. | github.create_pull_request shown with relevant parameters. |
| 5 | Click [Authorize]. | Dialog closes. Tool executes. Agent completes response. |
| 6 | Repeat steps 2-3. Click [Block] this time. | Authorization dialog appears. After clicking Block, tool does not execute. Agent acknowledges. |

## Expected Final State

Authorization dialog appears. After clicking Block, tool does not execute. Agent acknowledges.

## Pass/Fail Criteria

Pass:
- Authorization dialog appears in Chat context (not just Agent page)
- Dialog behavior is consistent: Authorize executes tool, Block prevents it
- Agent responds correctly in both scenarios in Chat

Fail:
- No dialog shown in Chat — tool executes immediately
- Dialog behavior differs from Agent page behavior
