---
id: ELITEA-3569
title: "Stale/Deleted Team, Channel, or Chat IDs Fail With a Clear \"Do Not Retry\" Signal"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3569: Stale/Deleted Team, Channel, or Chat IDs Fail With a Clear "Do Not Retry" Signal

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that a 404 from Graph (e.g. a chat or channel that no longer exists or isn't visible to the user) is surfaced with guidance rather than a generic error, so the calling agent doesn't blindly retry the same ID.

## Preconditions

- Teams toolkit enabled with an authorized credential
- A syntactically valid team/channel/chat ID that no longer exists or is no longer accessible to the signed-in user

## Test Data

- N/A (see Steps)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `find_chat_messages` with an ID that is syntactically valid but no longer exists/accessible | Error names the affected resource and advises against retrying with the same ID, directing to `list_chats` instead |
| 2 | Call `send_channel_message` with a similarly stale/inaccessible channel ID | Error names the affected resource and advises against retrying with the same ID, directing to `list_channels` instead |

## Expected Final State

Both calls fail deterministically with resource-specific, non-retryable guidance rather than a generic error.

## Pass/Fail Criteria

**Pass:**
- Both stale-ID calls name the resource and explicitly discourage retrying, pointing to the correct `list_*` tool

**Fail:**
- Either call returns a generic error, or fails to discourage retrying with the same stale ID
