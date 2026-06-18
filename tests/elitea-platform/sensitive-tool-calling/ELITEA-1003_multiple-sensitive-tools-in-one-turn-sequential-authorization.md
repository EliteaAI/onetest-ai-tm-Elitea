---
id: ELITEA-1003
title: "Multiple Sensitive Tools in One Turn — Sequential Authorization"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1003: Multiple Sensitive Tools in One Turn — Sequential Authorization

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an agent invokes multiple sensitive tools sequentially in a single prompt turn, each one triggers its own authorization dialog independently, one at a time.

## Preconditions

- Both github > create_pull_request and jira > create_issue are configured as sensitive
- Agent has both GitHub and Jira toolkits configured

## Test Data

- Prompt: 'Create a pull request in GitHub from feature/multi to main, and also create a Jira issue titled Test Multi Auth in project ELITEA'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send the prompt asking the agent to perform two sensitive actions: 'Create a pull request in GitHub from feature/multi to main, and also create a Jira issue titled Test Multi Auth in project ELITEA'. | Agent processes the request and the first sensitive tool is about to run. |
| 2 | Observe the first authorization dialog. | Dialog appears for the first sensitive tool (e.g., github.create_pull_request). |
| 3 | Click [Authorize] on the first dialog. | First dialog closes. First tool executes. |
| 4 | Observe the chat area again. | A second authorization dialog appears for the second sensitive tool (jira.create_issue). |
| 5 | Click [Authorize] on the second dialog. | Second dialog closes. Second tool executes. Agent completes its full response. |

## Expected Final State

Second dialog closes. Second tool executes. Agent completes its full response.

## Pass/Fail Criteria

Pass:
- Two separate dialogs appear, one per sensitive tool, in order
- First tool is not called until first Authorize is clicked
- Second tool is not called until second Authorize is clicked
- Agent completes normally after both are authorized

Fail:
- Only one dialog appears for two sensitive tools
- Both tools are intercepted in the same single dialog
- Second tool executes without showing a second dialog
