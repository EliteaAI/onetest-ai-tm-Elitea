---
id: ELITEA-1007
title: "Authorization Dialog — Content Completeness and Policy Message"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1007: Authorization Dialog — Content Completeness and Policy Message

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify all required visual elements of the authorization dialog are present and correctly rendered: title text, action name, expandable parameters accordion, policy message with company name interpolation, button styling, and warning border.

## Preconditions

- Sensitive tool github > create_pull_request is configured with company name EPAM
- Authorization dialog is currently displayed in the agent chat with parameters: repository: 'elitea/backend-api', title: 'feat: Test', base_branch: 'main', head_branch: 'feature/auth'

## Test Data

- Dialog under test: triggered by github.create_pull_request
- Company name: EPAM
- Parameters: repository: 'elitea/backend-api', title: 'feat: Test', base_branch: 'main', head_branch: 'feature/auth'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe the dialog header/title. | Title displays '⚠️ Sensitive Action Authorization Required'. |
| 2 | Observe the action name area below the header. | Shows 'Agent is about to perform:' followed by the action label (github.create_pull_request) in bold. |
| 3 | Observe the Parameters section below the action name. | Collapsible 'Parameters' accordion is visible and expanded by default showing key-value pairs: repository, title, base_branch, head_branch. |
| 4 | Click the 'Parameters' accordion header to collapse it. | Section collapses (fold arrow changes direction). |
| 5 | Click the 'Parameters' accordion header again to expand it. | Section expands again showing all parameters. |
| 6 | Observe the policy message. | Policy message reads: 'EPAM requires approval before running the sensitive action github.create_pull_request.' (or equivalent template with EPAM interpolated). |
| 7 | Clear company name in admin config. Save. Restart. Trigger the tool again. | Policy message uses 'Your organization' (or a configured default) instead of blank or erroring. |
| 8 | Observe the [Authorize] button styling. | Button is styled as a primary action (green or primary color with a checkmark icon). |
| 9 | Observe the [Block] button styling. | Button is styled as a secondary/destructive action (red or outlined with an X/reject icon). |
| 10 | Observe the dialog container border. | Dialog has an amber/warning colored border or warning-level visual indicator. |
| 11 | Observe the policy message text styling. | The policy message text is rendered in italic style. |

## Expected Final State

The policy message text is rendered in italic style.

## Pass/Fail Criteria

Pass:
- Title text exactly matches '\u26a0\ufe0f Sensitive Action Authorization Required'
- Action name is displayed prominently in bold
- Parameters accordion is visible, expanded by default, and toggles correctly
- Policy message correctly interpolates the configured company name
- Default fallback used when company name is empty
- Authorize button is primary style; Block button is secondary/destructive style
- Dialog has an amber/warning border

Fail:
- Any required element is missing or not rendered
- Parameters accordion does not expand/collapse
- Company name not interpolated (shows placeholder or blank)
- Buttons are unstyled or swapped
