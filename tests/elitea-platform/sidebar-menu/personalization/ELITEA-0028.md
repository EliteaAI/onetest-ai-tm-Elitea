---
id: ELITEA-0028
title: Verify changing Settings default doesn't modify existing conversation personas
priority: high
type: functional
module: settings
status: approved
execution_type: manual
tags:
  - personality
  - settings
  - backwards-compatibility
  - existing-conversations
requirements:
  - "#5394"
---

# Verify changing Settings default doesn't modify existing conversation personas

## Preconditions

- User is logged into EliteA platform
- User has access to Settings/Preferences with Default Personality
- User has multiple existing conversations with different personalities
- User can create new conversations

## Test Data

- Existing Conversation 1: Generic personality
- Existing Conversation 2: Bare personality with custom instructions "Be technical"
- Settings changes: Generic → Nerdy → Bare

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create conversation with Generic personality | Conversation 1 created with Generic |
| 2 | Send test message in Conversation 1 | Response with Generic personality |
| 3 | Create conversation with Bare personality | Conversation 2 created with Bare |
| 4 | Set custom instructions: "Be technical" | Instructions applied |
| 5 | Send test message in Conversation 2 | Response with Bare personality, technical |
| 6 | Navigate to Settings/Preferences | Settings page opens |
| 7 | Note current Default Personality (e.g., Generic) | Current default visible |
| 8 | Change Default Personality to "Nerdy" | Nerdy selected and saved |
| 9 | Return to Conversation 1 | Conversation 1 displays |
| 10 | Open Context Management modal | Modal opens |
| 11 | Verify personality still "Generic" (unchanged) | Generic still selected |
| 12 | Send message | Response still uses Generic personality |
| 13 | Switch to Conversation 2 | Conversation 2 displays |
| 14 | Open Context Management modal | Modal opens |
| 15 | Verify personality still "Bare" with custom instructions | Bare and instructions unchanged |
| 16 | Send message | Response still uses Bare with technical style |
| 17 | Create new conversation | New conversation opens |
| 18 | Verify new conversation uses "Nerdy" default | Context Management shows Nerdy |
| 19 | Change Settings default to "Bare" | Bare selected and saved |
| 20 | Verify existing conversations still unchanged | All maintain original personalities |

## Expected Final State

- Existing conversations retain their individual personality settings
- Default Personality change only affects newly created conversations
- No retroactive modification of existing conversation personalities
- Existing custom instructions preserved
- System respects conversation independence

## Pass/Fail Criteria

**Pass:**
- Existing conversations unchanged after default personality change
- Only new conversations use updated default
- All existing custom instructions preserved
- No retroactive personality changes
- System behavior predictable and consistent

**Fail:**
- Existing conversations modified by default change
- Personalities retroactively updated
- Custom instructions lost or changed
- Inconsistent or unpredictable behavior
- Errors or data corruption
