---
id: ELITEA-2950
title: "Verify send button behavior during active run"
priority: high
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, ui, send-button]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agent/LLM run active

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test message | "Test button state" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run | Run begins |
| 2 | Verify send button with empty composer | Send button disabled |
| 3 | Type text in composer | Send button enabled (cyan/active color) |
| 4 | Click send | Message queued, composer clears, button disables |
| 5 | Type new text | Button re-enables |
| 6 | Rapidly click send 3 times | Only ONE message queued |

## Expected Final State

- Button states transition correctly
- No duplicate messages from rapid clicks
- Composer clears after send

## Pass/Fail Criteria

**Pass:**
- Empty composer → button disabled
- Text present → button enabled
- After send → button disabled until new text
- Rapid clicks → only one message queued

**Fail:**
- Button enabled with empty composer
- Button stays enabled after send
- Multiple messages from rapid clicks
- Composer doesn't clear
