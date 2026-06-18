---
id: ELITEA-0600
title: "Support Assistant history panel renders all past conversations, most recent first"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0600: Support Assistant history panel renders all past conversations, most recent first

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Support Assistant history panel opens and displays all past support conversations ordered most-recent-first.

**Coverage:**
- History panel accessible via the 🕐 icon
- All past sessions for the user are listed
- Order is reverse-chronological (newest at top)

## Preconditions

- Logged in as a test user on {{base_url}}
- At least 3 completed Support Assistant conversations exist for this user (created on different dates)
- Support Assistant feature is enabled

## Test Data

- User with ≥3 prior support sessions (e.g., sessions created on Day 1, Day 2, Day 3)
- Support Assistant launcher selector: button.elitea-assistant-button

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to any ELITEA page (e.g., /app/chat) | Page loads successfully |
| 2 | Click the Support Assistant launcher (button, bottom-right or sidebar) | Support Assistant widget opens |
| 3 | Click the 'Chat history' (🕐) icon in the widget header | History panel/dropdown opens |
| 4 | Observe the full list of sessions shown | All past support conversations for the current user are listed — none are missing |
| 5 | Compare the order of sessions by their timestamps/dates | Sessions are ordered most-recent-first (Day 3 at top, Day 1 at bottom) |

## Expected Final State

Sessions are ordered most-recent-first (Day 3 at top, Day 1 at bottom)

## Pass/Fail Criteria

**Pass:**
- History panel opens without errors
- All user sessions are listed
- Order is newest-first

**Fail:**
- History panel fails to open or shows error
- Any past session is missing
- Sessions appear in wrong order (oldest first or random)
