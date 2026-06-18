---
id: ELITEA-0540
title: "Save and apply without changing content — triggers regeneration as retry"
priority: high
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0540: Save and apply without changing content — triggers regeneration as retry

**Module:** Edit User Message · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Save and apply without modifying the message still triggers a response regeneration (acts as a retry).

**Coverage:**
- Unmodified message re-submitted
- New response generated

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with a last user-assistant exchange

## Test Data

- Any existing conversation with a completed response

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Edit on the last user message. Note the original content. | Edit mode opens. Content is unchanged. |
| 2 | Without modifying any text, click "Save and apply". | Edit mode closes. Loading/streaming indicator appears — regeneration is triggered. |
| 3 | Wait for the new response to complete. | A new LLM response is generated and replaces the previous one. The user message content remains the same as before. |

## Expected Final State

A new LLM response is generated and replaces the previous one. The user message content remains the same as before.

## Pass/Fail Criteria

**Pass:**
- Regeneration is triggered even without content changes
- Previous response is replaced
- No error or blocking message appears

**Fail:**
- Save and apply is blocked when no changes exist
- No regeneration occurs
- Error message appears
