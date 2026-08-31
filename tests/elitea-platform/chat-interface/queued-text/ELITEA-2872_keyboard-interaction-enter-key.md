---
id: ELITEA-2872
title: "Verify Enter key sends interjection during active run"
priority: high
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, keyboard, ui]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agent/LLM run active
- Feature enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test message | "Test keyboard send" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run | Run begins |
| 2 | Type text in composer during active run | Text appears in composer |
| 3 | Press Enter key | Message sent and queued |
| 4 | Verify message in queue | Message appears in "Waiting messages" area |
| 5 | Verify composer state | Composer clears after send |
| 6 | Type new text | New text appears |
| 7 | Press Shift+Enter | New line created, message NOT sent |

## Expected Final State

- Enter sends interjection
- Shift+Enter creates new line
- Keyboard navigation works normally

## Pass/Fail Criteria

**Pass:**
- Enter sends message (same as click Send)
- Message queues correctly
- Composer clears
- Shift+Enter creates new line without sending

**Fail:**
- Enter doesn't send
- Shift+Enter sends instead of new line
- Composer doesn't clear
