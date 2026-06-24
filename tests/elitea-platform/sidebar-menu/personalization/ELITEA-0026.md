---
id: ELITEA-0026
title: "Verify Default Personality from Settings applies to newly created chats"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, settings, default-personality, new-conversation]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-0026: Verify Default Personality from Settings applies to newly created chats

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that Default Personality from Settings applies correctly to newly created chats

## Preconditions

- User is logged into EliteA platform
- User has access to Settings/Preferences page
- Default Personality setting exists in Settings
- User can create new conversations

## Test Data

- Default personality setting: Bare
- Custom instructions (if applicable): "Respond in bullet points"
- Test personalities: Generic, Bare, Nerdy

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings/Preferences page | Settings page opens |
| 2 | Locate "Default Personality" setting | Setting visible in appropriate section |
| 3 | Set default personality to "Generic" | Generic selected and saved |
| 4 | Create new conversation | New conversation opens |
| 5 | Open Context Management modal | Modal opens |
| 6 | Verify personality is "Generic" | Generic selected as default |
| 7 | Close conversation, return to Settings | Settings page opens |
| 8 | Change default personality to "Bare" | Bare selected |
| 9 | Set default custom instructions (if applicable): "Respond in bullet points" | Instructions entered and saved |
| 10 | Create new conversation | New conversation opens |
| 11 | Open Context Management modal | Modal opens |
| 12 | Verify personality is "Bare" | Bare selected as default |
| 13 | Verify custom instructions applied | Instructions field shows: "Respond in bullet points" |
| 14 | Send test message | Response follows Bare personality with bullet points |
| 15 | Create another new conversation | Second new conversation opens |
| 16 | Verify same default applies | Bare personality with custom instructions |

## Expected Final State

- Default Personality setting in Settings/Preferences works
- Newly created conversations inherit default personality
- Custom instructions (if applicable) applied to new conversations
- Setting persists across multiple new conversation creations
- No interference with existing conversations

## Pass/Fail Criteria

**Pass:**
- Default Personality setting found and functional
- New conversations use default personality from Settings
- Default custom instructions applied (if applicable)
- Setting works consistently for all new conversations
- Existing conversations unaffected

**Fail:**
- Default Personality setting missing or broken
- New conversations don't use default personality
- Default custom instructions not applied
- Inconsistent behavior across new conversations
- Existing conversations affected unexpectedly
