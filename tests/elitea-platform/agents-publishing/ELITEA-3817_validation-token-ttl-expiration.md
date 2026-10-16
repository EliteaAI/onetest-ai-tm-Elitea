---
id: ELITEA-3817
title: "Validation token TTL expiration"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with `models.applications.publish.post` permission
- Test agent with attached Skills (valid content)
- Timer/clock available to track 5-minute window

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "TTL Test Agent" |
| Skills | 1-2 valid Skills attached |
| Token TTL | 5 minutes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open agent with Skills | Agent loads |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for validation to pass | Result: **PASS** |
| 4 | Note current time | Record timestamp |
| 5 | Wait 5+ minutes without clicking Publish | Token TTL expires |
| 6 | Click **Publish** button | Error: "Validation expired" or "Token expired" |
| 7 | Verify re-validation required | Must re-validate before publishing |
| 8 | Re-validate immediately | Result: **PASS** |
| 9 | Click **Publish** within TTL window | "The agent has been published" toast |

## Expected Final State

Validation token expires after 5-minute TTL. Attempting to publish after expiration requires re-validation. Publishing within the TTL window succeeds.

## Pass/Fail Criteria

**Pass:**
- Token expires after 5-minute TTL
- Expired token produces clear error message
- Re-validation required after expiration
- Publishing within TTL window succeeds

**Fail:**
- Token doesn't expire after 5 minutes
- No error for expired token
- Can publish with expired token
