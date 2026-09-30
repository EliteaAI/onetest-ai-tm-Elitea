---
id: ELITEA-3561
title: "send_channel_message — Posts a New Channel Message and Replies to an Existing One"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3561: send_channel_message — Posts a New Channel Message and Replies to an Existing One

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `send_channel_message` can start a new channel post and reply to an existing post, correctly threading the reply.

## Preconditions

- Teams toolkit with `send_channel_message` enabled, linked to an authorized credential
- A valid team/channel the signed-in user can post to

## Test Data

- N/A (sequential scenario, see Steps)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `send_channel_message` for a valid team/channel with a `subject` | A new post is created with that subject; `message_id`/`thread_id` are returned |
| 2 | Call `send_channel_message` again with `reply_to_message_id` set to the post's ID | The reply is posted under that thread; any `subject` passed is ignored |
| 3 | Open the channel in Microsoft Teams and locate the original post | The reply is visible nested under the original post's thread |

## Expected Final State

The channel contains one new root post and one correctly threaded reply beneath it.

## Pass/Fail Criteria

**Pass:**
- New post and reply are both created correctly, and the reply appears nested under the original thread in Teams

**Fail:**
- The reply creates a separate root post instead of threading, or the reply's `subject` is not ignored
