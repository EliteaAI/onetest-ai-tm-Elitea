---
id: ELITEA-1009
title: "Admin Guardrails Configuration — Save and Persistence"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1009: Admin Guardrails Configuration — Save and Persistence

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify the complete admin configuration workflow: the Guardrails section is accessible, tools can be selected per toolkit, company name and message template can be set, the configuration saves successfully, and all values persist after page refresh.

## Preconditions

- Logged in as Platform Administrator
- Admin UI is accessible

## Test Data

- Toolkit to configure: github
- Tools to mark as sensitive: create_pull_request, delete_branch
- Company Name: EPAM
- Message template: (default or custom)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | 'Sensitive Action Tools' section is visible with tool selection, company name, and message template fields. |
| 2 | Expand or open the tool selection interface. Observe available toolkits. | All registered toolkit types are listed (e.g., github, jira, confluence). |
| 3 | Select the github toolkit. | Available tools for the GitHub toolkit are listed and selectable. |
| 4 | Check create_pull_request and delete_branch. | Both tools are marked as selected/checked. |
| 5 | Enter 'EPAM' in the Company Name field. | Field accepts the value. |
| 6 | Enter a custom message template or leave default. | Field accepts the value. |
| 7 | Click 'Save Configuration'. | Success notification shown. No error. |
| 8 | Refresh the browser page. Navigate back to Admin UI → Configuration → Guardrails. | Previously saved sensitive tools (create_pull_request, delete_branch), company name EPAM, and message template values are still displayed. |
| 9 | Uncheck create_pull_request. Save. Refresh. | create_pull_request is no longer checked. delete_branch remains checked. Configuration reflects the latest saved state. |

## Expected Final State

create_pull_request is no longer checked. delete_branch remains checked. Configuration reflects the latest saved state.

## Pass/Fail Criteria

Pass:
- Guardrails section is visible in Admin UI → Configuration
- All registered toolkits and their tools are browsable and selectable
- Check/uncheck toggles work cleanly
- Company name accepts text input
- Configuration saves with a success notification
- All values persist after page refresh
- Partial updates (uncheck one tool) are also persisted correctly

Fail:
- Guardrails section is absent or does not load
- Tools are not listed or cannot be selected
- Save fails with an error
- Values do not persist after refresh
