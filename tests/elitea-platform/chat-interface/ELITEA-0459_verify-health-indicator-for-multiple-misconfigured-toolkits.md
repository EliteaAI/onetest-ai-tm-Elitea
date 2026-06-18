---
id: ELITEA-0459
title: "Verify Health Indicator for Multiple Misconfigured Toolkits"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [credential-validation, toolkit-management, participants-panel, health-indicator, ux-improvement, chat-ui, 3709]
requirements: [GitHub Issue EliteaAI/elitea_issues#3709]
---
# ELITEA-0459: Verify Health Indicator for Multiple Misconfigured Toolkits

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when multiple toolkits in the same conversation are misconfigured, each displays its own health indicator with independent error message.

**Coverage:**
- Multiple toolkit health indicators
- Independent indicator display
- Per-toolkit error messaging
- Scalability of health indicator feature

## Preconditions

- User is logged in to ELITEA platform at {{base_url}}
- User has a conversation with 2 or more toolkit participants
- At least 2 of the toolkits have misconfiguration errors

## Test Data

- ELITEA URL: {{base_url}}
- Test conversation: Conversation with multiple toolkit participants
- Number of misconfigured toolkits: Minimum 2
- Expected indicators: One yellow/orange health indicator per misconfigured toolkit
- Expected messages: One "Misconfiguration errors found. Check the toolkit" message per misconfigured toolkit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to or create a conversation that includes 2 or more toolkit participants, with at least 2 having misconfiguration errors. | Conversation opens displaying all toolkit participants in the participants panel. |
| 2 | Locate all toolkit participants in the conversation that have misconfiguration errors. | At least 2 misconfigured toolkit participants are visible in the participants panel. |
| 3 | Observe each misconfigured toolkit participant for health indicator and error message. | Each misconfigured toolkit displays its own yellow/orange health indicator icon next to its name. |
| 4 | Verify that each misconfigured toolkit displays the complete error message 'Misconfiguration errors found. Check the toolkit' with clickable inline link. | Each misconfigured toolkit shows its own complete error message below its name, with 'Check the toolkit' portion styled as an inline clickable link. Indicators and messages appear independently for each toolkit. |
| 5 | Click the 'Check the toolkit' link for the first misconfigured toolkit. | User is navigated to the Canvas page for the first toolkit specifically. |
| 6 | Return to the conversation and click the 'Check the toolkit' link for the second misconfigured toolkit. | User is navigated to the Canvas page for the second toolkit specifically (not the first one). |

## Expected Final State

User is navigated to the Canvas page for the second toolkit specifically (not the first one).

## Pass/Fail Criteria

**Pass:**
- Each misconfigured toolkit displays its own health indicator
- Each misconfigured toolkit displays its own complete error message with clickable link
- Indicators and messages appear independently for each misconfigured toolkit
- Clicking each toolkit's link navigates to the correct toolkit's Canvas page
- Correctly configured toolkits (if any) do not show indicators

**Fail:**
- Only one health indicator appears when multiple toolkits are misconfigured
- Health indicators are shared or duplicated incorrectly
- Error messages are missing for some misconfigured toolkits
- Clicking links navigates to wrong toolkit Canvas page
- Indicators interfere with each other or display inconsistently
