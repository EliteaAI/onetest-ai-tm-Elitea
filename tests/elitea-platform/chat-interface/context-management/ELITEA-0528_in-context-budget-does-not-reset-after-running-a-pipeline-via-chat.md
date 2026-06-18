---
id: ELITEA-0528
title: "In-Context Budget Does Not Reset After Running a Pipeline via Chat"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:context-management, feat:pipelines, issue:4469, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4469]
---
# ELITEA-0528: In-Context Budget Does Not Reset After Running a Pipeline via Chat

**Module:** Context Management · **Priority:** High · **Type:** Functional

## Preconditions

- Logged in to {{base_url}}
- At least one pipeline exists in the project
- Chat conversation is open with the pipeline as a participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation and send 3–5 normal messages. | Messages are sent and responses received. In-context budget updates after each message (showing correct message count and token count). |
| 2 | Note the current in-context budget: message count (M) and token count (T). | Values M and T are recorded as baseline. |
| 3 | In the same Chat, select the pipeline (via participant or `/` mention) and run it. | Pipeline executes and returns a response. |
| 4 | Immediately check the in-context budget after the pipeline response. | Budget reflects the full conversation — message count is greater than 2 and token count reflects all prior messages plus the pipeline exchange. Budget has NOT reset to ~2 messages. |
| 5 | Send one more normal (non-pipeline) chat message. | Budget continues to increment normally. No sudden jump or restoration to a previously suppressed value. |

## Expected Final State

Budget continues to increment normally. No sudden jump or restoration to a previously suppressed value.

## Pass/Fail Criteria

**Pass:** In-context budget shows the full conversation history immediately after the pipeline runs — no reset to ~2 messages, no token count drop.
**Fail:** After the pipeline runs, the budget shows only ~2 messages and pipeline-only token usage; it only restores after sending another normal message.
