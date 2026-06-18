---
id: ELITEA-0594
title: "Session title in history is meaningful — no blank, null, or raw UUID"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0594: Session title in history is meaningful — no blank, null, or raw UUID

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify each history entry has a meaningful label — not blank, null, or a raw UUID.

**Coverage:**
- Title derived from first user message, session name, or creation date
- No blank or system-generated IDs shown to user

## Preconditions

- Logged in on {{base_url}}
- At least 3 sessions with different opening messages

## Test Data

- Session 1 first message: "How do I create an agent?"
- Session 2 first message: "I'm getting a 500 error"
- Session 3 first message: "Pipeline webhook configuration"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant history panel | All 3 sessions are listed |
| 2 | Read the label of each session | Each session label reflects the first user message, a human-readable title, or a date — not blank, null, or a UUID string |

## Expected Final State

Each session label reflects the first user message, a human-readable title, or a date — not blank, null, or a UUID string

## Pass/Fail Criteria

**Pass:**
- All history entries have meaningful, human-readable labels

**Fail:**
- Any entry shows blank label, null, raw UUID, or untranslated system string
