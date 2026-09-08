---
id: ELITEA-3325
title: "Chat Starters text is editable but adding, removing, or reordering is not supported in comparison"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions containing different Chat Starters

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 Chat Starters | ["How can I get started?", "What features are available?"] |
| Version 2 Chat Starters | ["Tell me about your capabilities", "How do I use this tool?", "Show me examples"] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Navigate to User Interaction section | Section loads with Welcome Message and Chat Starters |
| 3 | Locate Chat Starters fields in Version 1 column | Chat Starters list displays 2 items |
| 4 | Click on first Chat Starter text field ("How can I get started?") | Field is editable, cursor appears |
| 5 | Edit text to "How can I begin using this?" | Text updates successfully in the field |
| 6 | Verify there is NO "Add Chat Starter" button visible | No add button present |
| 7 | Verify there is NO "Remove Chat Starter" or delete button/icon | No remove button or X icon present |
| 8 | Attempt to drag Chat Starter items to reorder | No drag handle visible, items cannot be dragged |
| 9 | Verify Chat Starters list has exactly 2 items (matching saved version) | List shows only the 2 items from Version 1 |
| 10 | Verify Version 2 column shows 3 Chat Starters (matching its saved version) | Version 2 displays 3 Chat Starters |
| 11 | Edit one Chat Starter text in Version 1 and click Save for Version 1 | Save executes successfully |
| 12 | Close and reopen comparison modal | Modal opens with fresh data |
| 13 | Verify edited Chat Starter text was saved | Text shows "How can I begin using this?" |
| 14 | Verify Chat Starters list still has 2 items (order and membership unchanged) | Still exactly 2 items, same order as before |

## Expected Final State

Chat Starter text fields are editable and save successfully, but the list membership (count) and order remain fixed per version. No add/remove/reorder controls are available.

## Pass/Fail Criteria

**Pass:**
- Chat Starter text fields are editable
- Edited text saves successfully
- No "Add Chat Starter" button present
- No "Remove Chat Starter" button present
- No drag-to-reorder functionality
- List membership matches saved version (count unchanged after save)

**Fail:**
- Chat Starter text fields are read-only
- Add/remove buttons are present
- Drag-to-reorder is available
- List membership changes after text-only save
