---
id: ELITEA-0032
title: "Verify different users can have independent default personalities"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, settings, multi-user, isolation]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-0032: Verify different users can have independent default personalities

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that different users can have independent default personality settings

## Preconditions

- Two separate user accounts available (User A and User B)
- Both users can access Settings/Preferences
- Both users can create conversations
- Default Personality setting exists

## Test Data

- User A: Default personality = Generic
- User B: Default personality = Bare with custom instructions "Be concise"
- Test message: "What is artificial intelligence?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User A | User A logged in |
| 2 | Navigate to Settings/Preferences | Settings page opens |
| 3 | Set Default Personality to "Generic" | Generic selected and saved |
| 4 | Create new conversation as User A | Conversation opens |
| 5 | Verify personality is Generic | Context Management shows Generic |
| 6 | Send message: "What is artificial intelligence?" | Response with Generic personality |
| 7 | Log out User A | User A logged out |
| 8 | Log in as User B | User B logged in |
| 9 | Navigate to Settings/Preferences | Settings page opens |
| 10 | Set Default Personality to "Bare" | Bare selected |
| 11 | Set default custom instructions: "Be concise" | Instructions entered and saved |
| 12 | Create new conversation as User B | Conversation opens |
| 13 | Verify personality is Bare with custom instructions | Context Management shows Bare with "Be concise" |
| 14 | Send message: "What is artificial intelligence?" | Response with Bare personality, concise |
| 15 | Log out User B, log back in as User A | User A logged in |
| 16 | Verify User A's settings unchanged | Settings still show Generic |
| 17 | Create new conversation as User A | Conversation opens |
| 18 | Verify personality is Generic (not Bare) | Context Management shows Generic |
| 19 | Log out User A, log back in as User B | User B logged in |
| 20 | Verify User B's settings unchanged | Settings still show Bare with custom instructions |

## Expected Final State

- Each user has independent Default Personality setting
- User A's setting doesn't affect User B and vice versa
- Settings persist per user across login/logout
- Complete user isolation for personality preferences
- No cross-contamination between user accounts

## Pass/Fail Criteria

**Pass:**
- Each user has independent Default Personality setting
- Settings don't interfere between users
- Settings persist per user across sessions
- Complete isolation between user accounts
- No cross-contamination of preferences

**Fail:**
- Settings shared or confused between users
- One user's setting affects another user
- Settings lost after logout/login
- Cross-contamination of preferences
- Data leakage between user accounts
