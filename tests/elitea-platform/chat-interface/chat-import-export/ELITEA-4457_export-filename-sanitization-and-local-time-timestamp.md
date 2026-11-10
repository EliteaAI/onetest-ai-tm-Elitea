---
id: ELITEA-4457
title: "Export filename has disallowed characters sanitized and uses a local-time (not UTC) timestamp"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, issue:6903, p1]
requirements: ["EliteaAI/elitea_issues#6903"]
---

# ELITEA-4457: Export filename has disallowed characters sanitized and uses a local-time (not UTC) timestamp

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the downloaded export filename has every character disallowed in filenames replaced with `_`, and that the embedded timestamp reflects the user's local time, not UTC.

---

## Preconditions

- None beyond standard chat creation.

## Test Data

| Field | Value |
|-------|-------|
| First message | "Suggest?popular:armenian/song" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a chat. Send the first message "Suggest?popular:armenian/song". Send no other messages, attach nothing. Note the current local time. | Chat auto-named "Suggest?popular:armenian/song". |
| 2 | Export this chat "Without attachments". | Downloaded filename has every disallowed character (`? : /` etc.) replaced with `_`, e.g. `Suggest_popular_armenian_song_<YYYY-MM-DD_HH-mm-ss>.json` (or `.json.enc` if this environment encrypts exports). The embedded timestamp reflects the local time noted in step 1, not UTC. |

## Expected Final State

Filename sanitization is character-exact and the embedded timestamp is time-basis-correct (local time).

## Pass/Fail Criteria

**Pass:**
- Filename matches the sanitization rule exactly; timestamp reflects local time.

**Fail:**
- Any un-sanitized character left in the filename, or the timestamp reflecting UTC/wrong basis instead of local time.
