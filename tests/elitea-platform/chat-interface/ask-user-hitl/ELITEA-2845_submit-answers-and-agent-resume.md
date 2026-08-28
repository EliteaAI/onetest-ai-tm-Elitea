---
id: ELITEA-2845
title: "ask_user - Agent resumes execution after user submits all answers"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2845: ask_user - Agent resumes execution after user submits all answers

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after user submits all answers, agent resumes execution and produces follow-up response using the answers.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multiple questions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Create a project plan for me" |
| Answers | Project name: "Website Redesign", Timeline: "3 months", Budget: "$50,000" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send initial prompt requiring clarification | Agent triggers ask_user tool |
| 2 | Answer all questions in the clarifying card | All questions have answers |
| 3 | Click Submit or Final button | Card closes |
| 4 | Observe agent status | Agent resumes execution |
| 5 | Wait for agent response | Agent generates follow-up message |
| 6 | Verify response incorporates the submitted answers | Response uses "Website Redesign", "3 months", "$50,000" |
| 7 | Verify response is relevant to original request | Agent creates project plan using provided details |

## Expected Final State

Agent successfully resumes after answer submission and produces contextually relevant response using submitted answers.

## Pass/Fail Criteria

**Pass:** Agent resumes after submission, response incorporates all submitted answers, execution completes successfully

**Fail:** Agent does not resume, answers not used in response, execution hangs or errors
