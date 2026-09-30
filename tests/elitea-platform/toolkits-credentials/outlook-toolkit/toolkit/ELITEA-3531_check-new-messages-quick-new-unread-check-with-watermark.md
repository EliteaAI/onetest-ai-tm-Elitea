---
id: ELITEA-3531
title: "check_new_messages — Quick New/Unread Check With Watermark"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3531: check_new_messages — Quick New/Unread Check With Watermark

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `check_new_messages` correctly reports whether new/unread messages exist since a given watermark (`since` / `after_message_id`), and that "since wins" when both are provided (the documented "later wins" rule).

## Preconditions

- Test mailbox with a known message timeline and message IDs
- Toolkit with `check_new_messages` enabled

## Test Data

- `since`: timestamp earlier than the most recent test message
- `after_message_id`: an older message ID, earlier than `since`
- Both provided together (conflicting watermarks)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `check_new_messages` with only `since` set to a timestamp before the latest message | Reports that new messages exist |
| 2 | Invoke `check_new_messages` with only `after_message_id` set to an older message | Reports that new messages exist since that message |
| 3 | Invoke `check_new_messages` with both `since` and `after_message_id` set to different (conflicting) points, where `since` is the later/more restrictive watermark | Result reflects the `since` watermark ("later wins"), not `after_message_id` |

## Expected Final State

The reported new-message status accurately reflects the effective (later) watermark in all cases.

## Pass/Fail Criteria

**Pass:**
- Each watermark type independently reports correct new-message status
- When both are provided, `since` takes precedence as documented

**Fail:**
- Watermark comparison is inverted or ignored
- Providing both parameters produces an error instead of resolving per the "later wins" rule
