---
id: ELITEA-2672
title: "Mid-turn Input Disabled - Verify Legacy Behavior Preserved"
priority: critical
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:chat, feat:settings, eng:backend, eng:frontend, regression, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has permission to modify project settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

| Field | Value |
|-------|-------|
| Settings URL | `{{base_url}}/app/settings` |
| Chat URL | `{{base_url}}/app/chat` |
| Test prompt | "Write a comprehensive guide about artificial intelligence" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat section | Chat settings visible |
| 2 | Verify Mid-turn Input (Beta) toggle is present | Toggle is visible |
| 3 | Ensure toggle is OFF (disable if needed) | Toggle is in OFF position |
| 4 | Refresh the page | Page reloads |
| 5 | Navigate back to Settings → General → Chat section | Chat section displayed |
| 6 | Verify toggle state persisted | Toggle remains OFF |
| 7 | Navigate to Chat | Chat interface loads |
| 8 | Send the test prompt | Agent starts processing |
| 9 | While agent is generating response, observe input field | Input field is disabled or grayed out |
| 10 | Attempt to click/focus the input field | Input field does not accept focus |
| 11 | Attempt to type in the input field | No text appears, typing is blocked |
| 12 | Wait for agent to complete response | Agent completes normally |
| 13 | Verify input field becomes enabled | Input field is now enabled after turn completes |
| 14 | Send another message | New message can be sent normally |

## Expected Final State

When Mid-turn Input toggle is OFF:
- Input field remains disabled during agent execution
- User cannot type or send messages mid-turn
- Existing legacy behavior is preserved
- Input field re-enables after turn completes
- Normal messaging works as expected

## Pass/Fail Criteria

**Pass:**
- Toggle OFF state persists across page reload
- Input field disabled during agent execution when toggle OFF
- User cannot type or focus input field mid-turn
- Input field re-enables after turn completes
- Existing behavior unchanged, no regressions

**Fail:**
- Toggle state does not persist
- Input field enabled during agent execution when toggle OFF
- User can send mid-turn messages when feature disabled
- Input field remains disabled after turn completes
- Any regression in normal messaging flow
