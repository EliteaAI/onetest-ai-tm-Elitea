---
id: ELITEA-1014
title: "Authorize Action — Tool Executes with Original Parameters and Streaming Resumes"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1014: Authorize Action — Tool Executes with Original Parameters and Streaming Resumes

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking [Authorize] closes the dialog, executes the sensitive tool with the exact parameters shown, and allows the agent to complete its response normally with streaming resumed.

## Preconditions

- github > create_pull_request configured as sensitive
- Agent chat is open and the authorization dialog is currently displayed (result of triggering the sensitive tool)
- Dialog shows parameters: repository: "elitea/backend-api", title: "feat: Test", base_branch: "main", head_branch: "feature/test-branch"

## Test Data

- GitHub repo: elitea/backend-api (or a test repo where PRs can be verified)
- Expected side effect: A PR actually created in the specified repo after Authorize

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure the authorization dialog is visible with parameters shown. | Dialog is displayed. Chat input and Send button are disabled. |
| 2 | Click the [Authorize] button. | Dialog closes immediately. |
| 3 | Observe the chat area for agent streaming output. | Agent resumes streaming its response. No errors appearing. |
| 4 | Wait for agent response to complete. | Agent completes its full response acknowledging the tool result. |
| 5 | Verify the actual side effect: check in GitHub that a PR was created with exactly the parameters shown in the dialog. | PR exists in GitHub with the exact title, base, and head branch values shown in the dialog. |
| 6 | Verify the chat input and Send button are re-enabled after the agent finishes. | Input field is active. Send button is clickable. |
| 7 | Send a new test message in chat. | New message is sent and processed normally. |

## Expected Final State

New message is sent and processed normally.

## Pass/Fail Criteria

Pass:
- Dialog closes on clicking Authorize
- Tool executes with the exact parameters shown (PR created in GitHub with correct values)
- Agent streaming resumes without errors or duplicate content
- Chat input and Send button are re-enabled after completion
- A subsequent new message can be sent

Fail:
- Dialog does not close
- Tool does not execute (no PR created)
- Tool executes with different parameters than shown
- Agent streaming fails or produces duplicate content
- Chat input remains disabled after completion
