---
id: ELITEA-3814
title: "Validation token invalidation - skill content modified"
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
- Second browser/tab ready for concurrent modification test

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Token Test Agent" |
| Skill A | "Skill A" - valid instructions (150 chars) |
| Skill B | "Skill B" - valid instructions (150 chars) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open test agent with Skills A and B | Agent loads |
| 2 | Click ⋮ menu → **Publish** | Wizard opens |
| 3 | Complete Preparation step | Continue to Validation |
| 4 | Wait for validation to pass | Result: **PASS**, Publish button enabled |
| 5 | **DO NOT click Publish yet** | Stay on Validation step |
| 6 | In another tab, open the same agent | Agent loads in second tab |
| 7 | Edit "Skill A" instructions (add a sentence) | Save changes |
| 8 | Return to first tab with Publish wizard | Wizard still open |
| 9 | Click **Publish** button | Error: "Agent was modified since validation" |
| 10 | Verify token invalidation message | Message indicates content changed; re-validation required and publish button is Inactive |
| 11 | Click **Cancel** and attempt to validate again | Validation runs again |
| 12 | Wait for new validation | Result: **PASS** with new token |
| 13 | Click **Publish** | "The agent has been published" toast |

## Expected Final State

Modifying Skill content after validation passes invalidates the HMAC validation token. User must re-validate before publishing. After re-validation, publishing succeeds.

## Pass/Fail Criteria

**Pass:**
- Modifying any attached Skill content invalidates validation token
- Error message indicates content changed
- Re-validation required before publishing
- After re-validation, publish succeeds

**Fail:**
- Skill modification doesn't invalidate token
- No error when publishing with modified content
- Agent publishes with stale validation
