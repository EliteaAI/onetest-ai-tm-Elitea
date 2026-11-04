---
id: ELITEA-4247
title: Model override persists within chat session with Catalog skill
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, model-override, persistence, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4247: Model override persists within chat session with Catalog skill

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that model override persists for all messages within the current chat session with Catalog skill participant.

**Coverage:**
- Model override applies to all messages in session
- All responses use overridden model
- Override persists until chat is closed
- Network requests show overridden model

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open
- User has overridden the model (e.g., changed to "Opus 4.5")
- DevTools Network tab is open (optional for verification)

## Test Data

- Overridden model: "Opus 4.5"
- Test messages: "First message", "Second message", "Third message"
- Expected: All messages use overridden model

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In chat with Catalog skill, override model to "Opus 4.5" | Model selector shows "Opus 4.5" |
| 2 | Send message 1: "First message with override" | Message sent successfully |
| 3 | Wait for response 1 | Skill responds using "Opus 4.5" model |
| 4 | (Optional) Check DevTools Network tab for request 1 | Network request shows model: "Opus 4.5" |
| 5 | Send message 2: "Second message" | Message sent successfully |
| 6 | Wait for response 2 | Skill responds using "Opus 4.5" model |
| 7 | (Optional) Check DevTools Network tab for request 2 | Network request shows model: "Opus 4.5" |
| 8 | Send message 3: "Third message" | Message sent successfully |
| 9 | Wait for response 3 | Skill responds using "Opus 4.5" model |
| 10 | (Optional) Check DevTools Network tab for request 3 | Network request shows model: "Opus 4.5" |
| 11 | Verify all responses in chat | All 3 responses were generated using overridden model "Opus 4.5" |
| 12 | Check model selector still shows override | Model chip still displays "Opus 4.5" (override persists in session) |

## Expected Final State

Model override persists for entire chat session; all messages use overridden model; network requests confirm.

## Pass/Fail Criteria

**Pass:** All messages in session use overridden model, network requests confirm, override persists until chat closed.

**Fail:** Some messages use default model instead of override, or override resets mid-session.
