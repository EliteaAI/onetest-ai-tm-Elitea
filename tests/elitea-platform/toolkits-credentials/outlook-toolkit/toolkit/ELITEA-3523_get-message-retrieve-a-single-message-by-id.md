---
id: ELITEA-3523
title: "get_message — Retrieve a Single Message by ID"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3523: get_message — Retrieve a Single Message by ID

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `get_message` returns full message content (body, attachments metadata, headers) for a valid message ID and handles an invalid/nonexistent ID distinctly.

## Preconditions

- Toolkit with `get_message` enabled, linked to an authorized credential
- Known valid `message_id` from a prior `list_messages` call

## Test Data

- Valid `message_id`: obtained from `list_messages`
- Invalid `message_id`: `AAMkAD-invalid-id-000`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `get_message` with a valid `message_id` | Full message returned: subject, sender, body, received date, attachment metadata if present |
| 2 | Invoke `get_message` with an invalid/nonexistent `message_id` | A clear "message not found" error is returned, not a raw Graph 404 stack trace |

## Expected Final State

Valid IDs return complete message data; invalid IDs return a clear, handled not-found error.

## Pass/Fail Criteria

**Pass:**
- Valid message content is fully and correctly returned
- Invalid ID produces a clear, handled error

**Fail:**
- Valid message data is incomplete or incorrect
- Invalid ID produces an unhandled exception or silent empty response
