---
id: ELITEA-1505
title: "GH03 - Issue Workflow"
priority: critical
type: functional
module: github
status: ready
execution_type: automated
tags: [comment_on_issue, create_issue, workflow, github, issues, smoke]
requirements: []
---
# ELITEA-1505: GH03 - Issue Workflow

**Module:** Github · **Priority:** Critical · **Type:** Functional

**Objective:** Test full issue lifecycle: create issue, list issues, get specific issue, add various comment types (text, code, table), then close the issue.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Write access to the target repository (issue creation and commenting enabled)
Token has repo scope

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with issue creation enabled
Issue title: "GH03 Automated Test Issue — \u003ctimestamp\u003e"
Issue body: "This is an automated test issue. It will be closed automatically."
Comment 1: plain text — "Automated text comment"
Comment 2: code block — markdown code formatted snippet
Comment 3: table format — markdown table

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit and set GITHUB_TOOLKIT_NAME with write access token | Toolkit authenticated with write permissions |
| 2 | Invoke create_issue with title and body to create a new test issue | Issue created, valid issue number returned |
| 3 | Invoke get_issues to list repository issues and verify the new issue appears | New issue present in the issues list |
| 4 | Invoke get_issue with the issue number to retrieve issue details | Correct issue title and body returned |
| 5 | Invoke comment_on_issue with plain text comment on the issue | Text comment posted with comment ID returned |
| 6 | Invoke comment_on_issue with a code block comment (markdown formatted) | Code block comment posted successfully |
| 7 | Invoke comment_on_issue with a table formatted comment | Table comment posted successfully |
| 8 | Close the issue by updating its state to closed | Issue state changed to closed |
| 9 | Verify issue is closed by calling get_issue one more time | Issue state confirmed as closed |

## Expected Final State

Issue state confirmed as closed

## Pass/Fail Criteria

create_issue returns a valid issue number
get_issues includes the newly created issue
get_issue returns the correct title and body
All three comment_on_issue calls succeed
Issue successfully closed at end of workflow
No errors throughout the workflow
