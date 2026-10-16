---
id: ELITEA-3816
title: "Validation token invalidation - add/remove skill"
priority: critical
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
- Test agent with 2 attached Skills: "Skill A" and "Skill B"
- Both Skills have valid content passing all checks
- Additional "Skill C" available to add
- Second browser/tab ready for concurrent modification test

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Token Test Agent" |
| Skill A | "Skill A" - valid instructions (150 chars) |
| Skill B | "Skill B" - valid instructions (150 chars) |
| Skill C | "Skill C" - additional valid Skill to add |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open test agent with Skills A and B | 2 Skills attached |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for validation to pass | Result: **PASS** |
| 4 | **DO NOT click Publish** | Stay on Validation step |
| 5 | In another tab, add "Skill C" to the agent | 3 Skills now attached |
| 6 | Return to first tab, click **Publish** | Error: "Agent was modified since validation" |
| 7 | Verify token invalidation | Content hash mismatch due to added Skill |
| 8 | Restart wizard and re-validate | New validation with 3 Skills |
| 9 | Wait for validation to pass | Result: **PASS** |
| 10 | **DO NOT click Publish** | Stay on Validation step |
| 11 | In another tab, remove "Skill C" from agent | Back to 2 Skills |
| 12 | Return to first tab, click **Publish** | Error: "Agent was modified since validation" |
| 13 | Re-validate and publish | Publishes successfully |

## Expected Final State

Adding or removing Skills after validation passes invalidates the HMAC validation token. Re-validation is required before publishing.

## Pass/Fail Criteria

**Pass:**
- Adding a new Skill invalidates validation token
- Removing an existing Skill invalidates validation token
- Content hash mismatch error shown
- Re-validation required before publishing
- After re-validation, publish succeeds

**Fail:**
- Adding/removing Skills doesn't invalidate token
- Agent publishes with different Skill count than validated
