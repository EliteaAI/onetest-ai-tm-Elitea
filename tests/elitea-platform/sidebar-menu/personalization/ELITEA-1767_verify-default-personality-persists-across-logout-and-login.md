---
id: ELITEA-1767
title: "Verify Default Personality persists across logout and login"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, settings, persistence, session-management]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1767: Verify Default Personality persists across logout and login

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that Default Personality setting persists correctly across logout and login

## Preconditions

- User account with login credentials
- User has access to Settings/Preferences
- Default Personality setting exists
- User can log out and log back in

## Test Data

- Default personality: Bare
- Custom instructions (if applicable): "Provide step-by-step explanations"
- Test message: "Explain recursion"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to EliteA platform | User logged in successfully |
| 2 | Navigate to Settings/Preferences | Settings page opens |
| 3 | Set Default Personality to "Bare" | Bare selected |
| 4 | Set custom instructions: "Provide step-by-step explanations" | Instructions entered and saved |
| 5 | Verify settings saved successfully | Confirmation message or visual feedback |
| 6 | Create new conversation to verify default | Conversation opens with Bare personality |
| 7 | Verify custom instructions applied | Context Management shows instructions |
| 8 | Log out of EliteA platform | User logged out |
| 9 | Close browser completely (clear session) | Browser closed |
| 10 | Reopen browser and navigate to EliteA | Platform login page displays |
| 11 | Log in with same credentials | User logged in successfully |
| 12 | Navigate to Settings/Preferences | Settings page opens |
| 13 | Verify Default Personality still set to "Bare" | Bare selected in settings |
| 14 | Verify custom instructions preserved | Instructions field shows: "Provide step-by-step explanations" |
| 15 | Create new conversation | Conversation opens |
| 16 | Verify Bare personality with custom instructions | Context Management shows Bare with instructions |
| 17 | Send message: "Explain recursion" | Response follows Bare personality with step-by-step format |

## Expected Final State

- Default Personality setting persists across logout/login
- Custom instructions preserved after logout/login
- Setting survives complete browser session closure
- New conversations after login use saved default
- No data loss or reset to system defaults

## Pass/Fail Criteria

**Pass:**
- Default Personality persists after logout
- Custom instructions preserved after logout
- Settings survive browser session closure
- New conversations after login use saved default
- No data loss or unexpected resets

**Fail:**
- Default Personality lost after logout
- Custom instructions lost after logout
- Settings reset to defaults after browser close
- New conversations don't use saved default
- Data loss or corruption after logout/login
