---
id: ELITEA-3744
title: "Context Window Mode (Balanced/Full) Set in Personal Settings Reflects in New Chat's Context Management Widget"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_context_management.TestContextManagementSettings.test_context_budget_reflects_profile_max_tokens[10k_tokens]
  - tests.ui.chat.test_context_management.TestContextManagementSettings.test_context_budget_reflects_profile_max_tokens[32k_tokens]
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---
# ELITEA-3744: Context Window Mode Set in Personal Settings Reflects in New Chat's Context Management Widget

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Rewrite note (2026-11-12):** Original case asserted the Context Budget panel displays the exact numeric "Max Context Tokens" value from profile settings (10k/32k variants). That field was removed by EliteaAI/elitea_issues#6898 (replaced with a Balanced/Full "Context window" radio, a single personal setting applied across all projects). This rewrite covers the equivalent intent — personal setting propagates correctly to a new chat — under the new mechanism. **Automation test IDs above are stale and will fail; they need a corresponding rewrite in `tests.ui.chat.test_context_management` before this is re-marked `ready`.**

**Objective:** Verify that the Context window mode (Balanced/Full) configured in the user's personal settings propagates correctly into a brand-new chat conversation, and that updating the setting is reflected without stale caching.

**Coverage:**
- User sets Context window mode to Full in personal settings (Settings → Memory)
- User creates a new chat conversation and sends a message
- Context Management widget shows Window: Full and the model's actual full context window as Total window
- Switching the personal setting back to Balanced and creating another new chat shows Window: Balanced, Total window capped at 272,000

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- AI model is available for generating responses
- Context Management feature is enabled in the platform

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}` |
| Mode variant 1 | Full |
| Mode variant 2 | Balanced |
| Test message | `at_ctx_window_test_full` / `at_ctx_window_test_balanced` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Memory (Personalization). | Settings page loads with a "Context window" radio group (Balanced/Full). |
| 2 | Select "Full". Wait for autosave. Reload the page. | After reload, "Full" remains selected — confirming the value was persisted. |
| 3 | Navigate to Chat. Click 'Create Conversation' to start a new conversation. | A fresh conversation opens with no messages. |
| 4 | Type a short test message and send it. Wait for AI response (up to 30 seconds). | AI responds. The Context Management widget becomes visible. |
| 5 | Inspect the widget's Window mode and Total window value. | Window shows "Full"; Total window equals the active model's actual full context window (not a fixed numeric profile value). |
| 6 | Repeat steps 2–5 with the personal setting set to "Balanced". | Window shows "Balanced"; Total window is capped at 272,000 (or the model's window, whichever is smaller) — confirming the updated value propagates without stale caching. |

## Expected Final State

The Context Management widget in a new chat reflects the exact Context window mode configured in personal settings for both tested values (Full and Balanced).

## Pass/Fail Criteria

**Pass:**
- Personal setting autosaves window mode (verified by page reload)
- Context Management widget appears after first message
- Widget displays the matching window mode and correct Total window for both Full and Balanced
- No stale/cached value from a previous setting

**Fail:**
- Widget does not appear after sending a message
- Widget shows a different window mode or incorrect Total window
- Setting does not persist after page reload
