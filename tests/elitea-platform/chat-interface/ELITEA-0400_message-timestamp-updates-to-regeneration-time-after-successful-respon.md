---
id: ELITEA-0400
title: "Message Timestamp Updates to Regeneration Time After Successful Response Regeneration"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [issue:4833, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4833]
---
# ELITEA-0400: Message Timestamp Updates to Regeneration Time After Successful Response Regeneration

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

## Preconditions

- Logged in to {{base_url}}
- A conversation exists with at least one assistant response that has a visible timestamp

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation that already has at least one assistant response (e.g. an old conversation from several minutes or days ago). | The conversation is open. The assistant message shows an old timestamp (e.g. "20 minutes ago" or "2 months ago"). |
| 2 | Note the current timestamp shown on the last assistant message and the timestamp on the corresponding user message. | Both timestamps are recorded as baseline. |
| 3 | Trigger regeneration on the last assistant message (click the Regenerate button). Wait for the regeneration to complete successfully. | A new response is generated and displayed. |
| 4 | Check the timestamp on the regenerated assistant message. | The assistant message timestamp is updated to reflect the time of regeneration (e.g. "just now"). |
| 5 | Check the timestamp on the original user message. | The user message timestamp is unchanged — it still shows the original send time. |

## Expected Final State

The user message timestamp is unchanged — it still shows the original send time.

## Pass/Fail Criteria

**Pass:**
- After regeneration, the assistant message timestamp updates to reflect the regeneration time (e.g. "just now")
- The user message timestamp remains unchanged

**Fail:**
- The assistant message still shows the original timestamp (e.g. "20 minutes ago" or "2 months ago") after regeneration completes
