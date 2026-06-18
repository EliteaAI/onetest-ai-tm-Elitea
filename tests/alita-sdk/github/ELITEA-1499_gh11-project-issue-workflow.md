---
id: ELITEA-1499
title: "GH11 - Project Issue Workflow"
priority: high
type: functional
module: github
status: ready
execution_type: automated
tags: [create_issue_on_project, search_project_issues, projects, workflow, github]
requirements: []
---
# ELITEA-1499: GH11 - Project Issue Workflow

**Module:** Github · **Priority:** High · **Type:** Functional

**Objective:** Test project issue lifecycle: create issue on project, search project issues, list project issues, update issue on project, add comment, then close.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Write access to target repository and project
GitHub Project exists and is linked to the repository
Token has project scope

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with GitHub Project linked
GITHUB_PROJECT_ID or project name: required project identifier
Issue title: "GH11 Project Workflow Test Issue — \u003ctimestamp\u003e"
Issue body: "Automated project issue test"
Update field: project status or priority field
Token scopes: repo + project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit with write access and set GITHUB_TOOLKIT_NAME | Toolkit authenticated with project and repo scope |
| 2 | Invoke create_issue_on_project with title and body to create a test issue on the GitHub Project | Issue created with valid issue number returned |
| 3 | Invoke search_project_issues with a query matching the newly created issue title | Search results include the newly created issue |
| 4 | Invoke list_project_issues to list all issues in the project | Issue list includes the newly created issue |
| 5 | Invoke update_issue_on_project to modify the issue (e.g., change priority or status field) | Issue updated on project board successfully |
| 6 | Post a comment on the issue using comment_on_issue | Comment posted with comment ID returned |
| 7 | Close the issue by updating its state to closed | Issue closed without error |
| 8 | Verify issue is closed by retrieving it and confirming state=closed | Issue state confirmed as closed |

## Expected Final State

Issue state confirmed as closed

## Pass/Fail Criteria

create_issue_on_project returns a valid issue number
search_project_issues finds the created issue
list_project_issues includes the created issue
update_issue_on_project modifies the issue successfully
Comment posted and issue closed without errors
