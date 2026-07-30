---
id: ELITEA-2594
title: "Trace steps endpoint handles invalid message_group_id"
priority: medium
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:backend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5727]
---
# ELITEA-2594: Trace steps endpoint handles invalid message_group_id

**Module:** Trace Steps API · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the trace steps endpoint handles invalid or non-existent message_group_id parameters gracefully.

**Coverage:**
- Non-existent ID returns appropriate error
- Invalid format ID returns appropriate error
- No server crashes or 500 errors

## Preconditions

- Logged in to {{base_url}}
- API testing tool available (Postman, curl)

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `GET /api/v2/elitea_core/message_traces/{workspace}/{project}/{conversation_id}` |
| Non-existent ID | 999999999 |
| Invalid format (string) | "abc" |
| Invalid format (negative) | -1 |
| Empty parameter | "" (no value) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `/message_traces/...?message_group_ids=999999999` (non-existent ID) | Returns `200 OK` with `{"total": null, "rows": []}` (empty array) |
| 2 | Verify no 500 error, response is valid JSON | No server crash, graceful handling |
| 3 | Call `/message_traces/...?message_group_ids=abc` (string instead of int) | Returns error: `{"error": "message_group_ids must contain integers"}` |
| 4 | Verify appropriate error message returned | Clear validation message, no 500 error |
| 5 | Call `/message_traces/...?message_group_ids=-1` (negative number) | Returns error: `{"error": "message_group_ids must contain 1-200 positive integers"}` |
| 6 | Verify validation rejects negative IDs | Clear error message indicating positive integers required |
| 7 | Call `/message_traces/...?message_group_ids=` (empty parameter) | Returns all message groups for the conversation (not an error) |
| 8 | Document: empty param is a valid use case | Returns data (feature, not bug) |

## Expected Final State

Invalid `message_group_id` values are handled gracefully with clear validation error messages. Non-existent IDs return empty array. Empty parameter returns all message groups (valid use case). No 500 server errors occur.

## Pass/Fail Criteria

**Pass:**
- Non-existent ID (999999999): `200 OK` + `"rows": []` (empty array)
- String format (abc): Error `"message_group_ids must contain integers"`
- Negative ID (-1): Error `"message_group_ids must contain 1-200 positive integers"`
- Empty parameter: Returns all message groups for conversation (valid behavior)
- No 500 internal server errors
- Clear, actionable error messages

**Fail:**
- 500 internal server error on any input
- Server crash
- Unclear or missing error messages
- Non-existent ID returns error instead of empty array
