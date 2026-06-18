---
id: ELITEA-0100
title: "Descriptive error message is displayed when rate limit is exceeded"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, issue:3721, r-2.0.1, 3721]
requirements: [ProjectAlita/projectalita.github.io#3721]
---
# ELITEA-0100: Descriptive error message is displayed when rate limit is exceeded

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the per-minute or per-hour rate limit is exceeded, the user receives a descriptive error message instead of the generic "Too Many Requests" message, including rate limit type and error code details.

**Coverage:**
- Generic "Too Many Requests" message is replaced with a descriptive message
- Error message includes the type of rate limit exceeded (e.g., per-minute, per-hour)
- Error message includes the response error code or additional diagnostic information
- Error appears in the chat area where the user triggered the request

## Preconditions

- Logged in to {{base_url}} with a valid user account
- Access to an Agent or Chat configured with an LLM model
- Ability to trigger rate limit (send rapid successive requests or use an account close to its limit)

## Test Data

- LLM model: any (e.g., gpt-4o, claude-3-5-sonnet)
- Trigger: send multiple rapid messages in quick succession to exceed the per-minute rate limit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat or open an existing Agent. | Chat/Agent page opens. |
| 2 | Send multiple rapid successive messages to trigger the per-minute rate limit. | Rate limit is exceeded and an error response is returned. |
| 3 | Observe the error message displayed in the chat area. |  |
| 4 | Verify the error message includes the type of rate limit exceeded (e.g., "per-minute rate limit exceeded"). | Rate limit type is clearly stated in the error message. |
| 5 | Verify the error message includes an error code or additional diagnostic details useful for troubleshooting. | Error code (e.g., 429) and/or additional context is visible in the error message. |

## Expected Final State

Error code (e.g., 429) and/or additional context is visible in the error message.

## Pass/Fail Criteria

**Pass:**
- Error message is descriptive and not the generic "Too Many Requests" string
- Rate limit type (per-minute/per-hour) is stated in the message
- Error code or additional diagnostic info is included

**Fail:**
- Error message still reads only "Too Many Requests" with no additional context
- No error code or rate limit type is provided to the user
