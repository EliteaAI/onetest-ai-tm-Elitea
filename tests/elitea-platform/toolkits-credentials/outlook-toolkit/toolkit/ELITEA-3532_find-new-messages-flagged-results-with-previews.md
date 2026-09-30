---
id: ELITEA-3532
title: "find_new_messages — Flagged Results With Previews"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3532: find_new_messages — Flagged Results With Previews

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `find_new_messages` returns the actual matching messages (not just a boolean), honors `only_new`/`unread_only` flags, and includes a body preview when `include_preview=True`.

## Preconditions

- Test mailbox with a mix of read/unread messages, including at least one unread
- Toolkit with `find_new_messages` enabled

## Test Data

- `only_new = True`, `unread_only = False`, `include_preview = True`
- `only_new = False`, `unread_only = True`, `include_preview = False`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `find_new_messages` with `only_new=True`, `include_preview=True` | Returns new messages since the reference point, each including a short body preview |
| 2 | Invoke `find_new_messages` with `unread_only=True`, `include_preview=False` | Returns only unread messages, with no preview field populated |
| 3 | Compare the two result sets against the known mailbox state | Each flag combination returns the correct subset of messages |

## Expected Final State

Result sets accurately reflect the requested flag combinations.

## Pass/Fail Criteria

**Pass:**
- `only_new`/`unread_only` correctly filter the result set independently
- `include_preview` correctly toggles whether a body preview is included

**Fail:**
- Filters are ignored or combined incorrectly
- Preview is included/excluded contrary to the flag
