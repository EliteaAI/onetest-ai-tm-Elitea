---
id: ELITEA-0018
title: Verify API returns no legacy description field for existing users
priority: critical
type: functional
module: api
status: approved
execution_type: manual
tags:
  - personality
  - api
  - backwards-compatibility
  - migration
  - bug-env:next
  - bug-env:dev
requirements:
  - "#5394"
---

# Verify API returns no legacy description field for existing users

## Preconditions

- User account existed before Bare personality feature deployment
- User has API access credentials
- User can make API calls to conversation/user endpoints
- API documentation available for reference

## Test Data

- Existing user account ID
- API endpoint: `/api/v1/conversations/{id}` or equivalent user profile endpoint
- Valid authentication token

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Authenticate with API using existing user credentials | Authentication successful, token received |
| 2 | Make GET request to user profile endpoint | User profile data returned |
| 3 | Inspect JSON response structure | Response contains user profile fields |
| 4 | Search for "description" field in response | No "description" field present in JSON |
| 5 | Verify "personality" field exists | "personality" field present with value |
| 6 | Create new conversation via API | Conversation created successfully |
| 7 | Make GET request to conversation endpoint | Conversation data returned |
| 8 | Inspect conversation JSON response | Response contains conversation fields |
| 9 | Search for "description" field in conversation data | No "description" field present |
| 10 | Verify personality-related fields only | Only new personality schema fields present (personality, custom_instructions) |

## Expected Final State

- API responses contain no legacy "description" field
- Only new personality schema fields present (personality, custom_instructions)
- Existing users migrated to new schema
- API responses clean and consistent
- No data loss during migration

## Pass/Fail Criteria

**Pass:**
- No "description" field in any API response
- "personality" field present with appropriate value
- API responses follow new schema consistently
- No errors or unexpected fields
- Data integrity maintained

**Fail:**
- "description" field still present in API responses
- Missing "personality" field
- Mixed old/new schema in responses
- API errors or inconsistent responses
- Data loss or corruption
