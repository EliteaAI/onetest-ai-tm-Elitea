---
id: ELITEA-0460
title: "Verify Health Indicator in Conversation List Preview"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [credential-validation, toolkit-management, participants-panel, health-indicator, ux-improvement, chat-ui, 3709]
requirements: [GitHub Issue EliteaAI/elitea_issues#3709]
---
# ELITEA-0460: Verify Health Indicator in Conversation List Preview

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations containing misconfigured toolkits show an indicator in the conversation list/sidebar.

**Coverage:**
- Conversation list indicator display
- Sidebar preview functionality
- Visual cue in conversation overview
- Quick identification of problematic conversations

## Preconditions

- User is logged in to ELITEA platform at {{base_url}}
- User has multiple conversations
- At least one conversation contains a misconfigured toolkit
- At least one conversation contains only correctly configured toolkits (or no toolkits)

## Test Data

- ELITEA URL: {{base_url}}
- Test conversations: Multiple conversations, including at least one with misconfigured toolkit
- Conversation list: Sidebar or main view showing list of conversations
- Expected indicator: Icon, badge, or visual cue in conversation list entry
- Control conversation: Conversation without misconfigured toolkits

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the ELITEA main view where the conversation list/sidebar is visible. | Conversation list or sidebar is displayed showing all user conversations. |
| 2 | Locate the conversation entry that contains a misconfigured toolkit participant in the conversation list. | Conversation entry is visible in the list with conversation name or preview. |
| 3 | Observe the conversation list entry for any visual indicators (icon, badge, color, or other cue) that signify configuration issues. | The conversation entry shows some indication (icon, badge, warning symbol, or other visual cue) that a toolkit has configuration issues. |
| 4 | Compare with conversation entries that do not contain misconfigured toolkits. | Conversation entries without misconfigured toolkits do not display the health-related indicator, confirming the indicator is specific to conversations with toolkit issues. |

## Expected Final State

Conversation entries without misconfigured toolkits do not display the health-related indicator, confirming the indicator is specific to conversations with toolkit issues.

## Pass/Fail Criteria

**Pass:**
- Conversation list entry shows visual indicator (icon, badge, or cue) for conversations with misconfigured toolkits
- Indicator is clearly visible and distinguishable in the conversation list
- Indicator allows quick identification of problematic conversations
- Conversations without misconfigured toolkits do not show the indicator

**Fail:**
- No indicator appears in conversation list for conversations with misconfigured toolkits
- Indicator is not visible or distinguishable
- Indicator appears for conversations without toolkit issues (false positive)
- User cannot identify problematic conversations from the list view
