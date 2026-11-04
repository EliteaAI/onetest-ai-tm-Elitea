---
id: ELITEA-4256
title: User can override model for Catalog skill participant (per chat)
priority: critical
type: regression
module: elitea-platform
status: draft
execution_type: manual
tags: [feat:skills, catalog, chat, model-override, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922, EliteaAI/elitea_issues#7219]
---
# ELITEA-4256: User can override model for Catalog skill participant (per chat) (Regression)

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that user can override the LLM model for Catalog skill participant in chat, and override applies only to current chat without changing published skill settings.

**Coverage:**
- User can select different model
- Override applies to current chat only
- Published skill settings NOT changed
- Override persists within chat session

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open
- Skill has default model configured (e.g., "Dial-Anthropic-Sonnet-5.5")
- User has permission to change models

## Test Data

- Default model: "Dial-Anthropic-Sonnet-5.5" (or skill's configured model)
- Override model: "Opus 4.5" (or any different available model)
- Expected: Override applies to chat, skill settings unchanged

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat with Catalog skill participant | Chat opens, skill visible in SKILLS section |
| 2 | Check current model in Context Management / LLM Settings | Model chip shows skill's default configured model (e.g., "Dial-Anthropic-Sonnet-5.5") |
| 3 | Click on the model selector chip | Model picker dropdown opens showing available models |
| 4 | Select a different model (e.g., "Opus 4.5") | Model selection updates |
| 5 | Observe the model chip after selection | Model chip now shows "Opus 4.5" (overridden model) |
| 6 | Send message: "Hello with new model" | Message sends successfully |
| 7 | Wait for response and observe Network tab (DevTools) | Response generated using overridden model "Opus 4.5", network request shows overridden model |
| 8 | Close the chat (navigate away) | Chat closes |
| 9 | Reopen the same chat from Chats list | Chat reopens |
| 10 | Check the model selector again | Model resets to skill's default (e.g., "Dial-Anthropic-Sonnet-5.5"), override was session-only |

## Expected Final State

User can override model per chat; override applies to current session only; published skill settings unchanged.

## Pass/Fail Criteria

**Pass:** Model override works, applies to current chat, resets after close/reopen, published skill unchanged.

**Fail:** Cannot override model, override persists after reopen, or published skill settings changed.
