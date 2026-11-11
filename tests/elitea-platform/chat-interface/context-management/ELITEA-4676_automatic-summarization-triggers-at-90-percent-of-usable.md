---
id: ELITEA-4676
title: "Automatic Summarization Triggers at 90 Percent of Usable Input With Three-Tier Coloring"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Automatic Summarization is enabled for the chat under test
- Existing manual test ELITEA-0449 is known to be stale (built around the removed `Max Context Tokens` field and an old >100%/≤100% two-tier coloring) and must NOT be relied on as-is; this case supersedes its intent under the new mechanism

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Window mode | Balanced (or a model with a small enough window to reach the threshold quickly) |
| Context-overflow trigger message | A long, detailed request (e.g., "Give me an extensive biography of a historical figure") |
| Follow-up message | A short message (e.g., "Hello") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat with Automatic Summarization enabled. Note the usable input (available window minus reserved output) shown or inferable from the Context management card. | Baseline usable input is recorded. |
| 2 | Send messages until usage crosses 90% of usable input. | The Context management widget and the collapsed ring both switch to a "warning" color state at/after 90% usage — not only at 100% as in the old behavior. |
| 3 | Continue sending messages until automatic summarization fires. | Summarization triggers once the next-request estimate reaches the 90%-of-usable-input compaction threshold. |
| 4 | Immediately after summarization completes (no extra message sent), observe the Context management widget token count. | Token count drops immediately after summarization, without needing another message. |
| 5 | Observe the collapsed ring/status indicator immediately after summarization. | The indicator transitions out of the warning/error color in the same turn that triggered summarization. |
| 6 | Check the Summaries count and the preserved recent messages. | Summaries count increases by 1; the configured number of recent messages remains visible/preserved. |

## Expected Final State

The compaction threshold correctly fires at 90% of usable input (not 100%), the widget and ring both reflect a three-tier color state (normal/warning/error), and both update immediately after summarization completes without requiring another message.

## Pass/Fail Criteria

**Pass:**
- Warning color appears at/after 90% of usable input, before 100%
- Summarization triggers based on the 90% compaction threshold
- Widget token count and ring color both update immediately post-summarization, in the same turn
- Summaries count increases and recent messages are preserved

**Fail:**
- Warning color only appears at/after 100% (old behavior persisting)
- Summarization does not trigger at the expected 90% threshold
- Widget or ring requires an additional message to reflect the post-summarization state
