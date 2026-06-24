---
id: ELITEA-0019
title: "Verify API returns no description field for newly created users"
priority: critical
type: functional
module: api
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, api, new-user, schema-validation, bug-env:next, bug-env:dev]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-0019: Verify API returns no description field for newly created users

**Module:** API · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that API returns no description field for newly created users

## Preconditions

- Ability to create new user accounts
- API access for user creation and profile endpoints
- Test environment with Bare personality feature deployed
- API documentation available

## Test Data

- New user registration data:
  - Email: `testuser_bare_${timestamp}@example.com`
  - Password: (valid test password)
- API endpoints: `/api/v1/auth/register`, `/api/v1/users/me`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Make POST request to user registration endpoint | New user created successfully |
| 2 | Receive registration response | Response contains user ID and success status |
| 3 | Inspect registration response JSON | No "description" field in response |
| 4 | Authenticate with new user credentials | Authentication successful, token received |
| 5 | Make GET request to user profile endpoint (/users/me) | User profile data returned |
| 6 | Inspect user profile JSON response | Response follows new schema |
| 7 | Verify no "description" field present | No "description" field in JSON |
| 8 | Verify "personality" field exists | "personality" field present (likely "generic" or "none" as default) |
| 9 | Create conversation with new user account | Conversation created successfully |
| 10 | Retrieve conversation data via API | Conversation data returned |
| 11 | Verify conversation uses new schema | No "description" field, only personality fields |
| 12 | Update user personality via API (set to "bare") | Update successful |
| 13 | Retrieve updated user profile | Updated personality reflected, no description field |

## Expected Final State

- New users created with new personality schema only
- No legacy "description" field in any API response
- "personality" field present in all relevant endpoints
- New user accounts fully compatible with Bare personality
- Clean schema without legacy fields

## Pass/Fail Criteria

**Pass:**
- New user created successfully
- No "description" field in any API response for new user
- "personality" field present and functional
- Can set and update personality (including Bare) via API
- API responses consistent with new schema

**Fail:**
- "description" field appears in any API response
- Missing "personality" field
- Cannot set Bare personality for new user
- API errors during user creation or profile retrieval
- Schema inconsistencies
