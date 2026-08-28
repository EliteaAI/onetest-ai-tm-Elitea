---
id: ELITEA-2847
title: "ask_user - Free-text 'Other' option available and captured correctly"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2847: ask_user - Free-text 'Other' option available and captured correctly

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify free-text "Other" option is available for applicable questions and answer is captured correctly.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with questions that include predefined options

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question type | Single-select or multi-select with "Other" option |
| Other value | Custom text input |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with question offering predefined choices | Question with options appears |
| 2 | Verify "Other" option is visible in the choices | "Other" option is present |
| 3 | Select "Other" option | Free-text input field appears |
| 4 | Enter custom text in the "Other" field | Text is accepted (e.g., "Custom location: Mars") |
| 5 | Verify Next button becomes enabled after entering text | Next button is enabled |
| 6 | Navigate to next question and back | Return to question with "Other" |
| 7 | Verify custom text is preserved | "Other" remains selected, custom text is visible |
| 8 | Complete and submit all questions | Card closes |
| 9 | Verify agent response uses the custom "Other" value | Agent response references "Mars" or custom value |

## Expected Final State

"Other" option works correctly, free-text input is captured, preserved on navigation, and used by agent.

## Pass/Fail Criteria

**Pass:** "Other" option visible, free-text field appears when selected, custom value captured and used by agent

**Fail:** "Other" option missing, free-text field not functional, custom value lost or not used
