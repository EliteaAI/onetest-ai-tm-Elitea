---
id: ELITEA-3837
title: "Edge case - skill instruction length boundaries"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with publish permissions
- Test agent created for edge case testing
- Skills with boundary-condition content prepared

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill 1 | "Boundary Length Skill" - Instructions at exactly minimum length (e.g., 100 chars) |
| Skill 2 | "Max Length Skill" - Instructions at maximum allowed length |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill with exactly minimum length instructions | Skill created |
| 2 | Attach to test agent | Skill attached |
| 3 | Click ⋮ menu → **Publish** → validate | Validation runs |
| 4 | Verify length check result | **PASS** - exactly at boundary passes |
| 5 | Edit Skill: remove 1 character (below minimum) | Save change |
| 6 | Re-validate | **FAIL** - CRITICAL for length violation |
| 7 | Edit Skill: add 1 character back + 1 more (above minimum) | Save change |
| 8 | Re-validate | **PASS** - above minimum passes |
| 9 | Replace with "Max Length Skill" | Skill with maximum content |
| 10 | Validate | **PASS** - max length accepted |
| 11 | Verify no timeout or truncation | Validation completes normally |

## Expected Final State

Validation correctly handles Skill instructions at exact minimum and maximum length boundaries. Exactly-at-minimum passes, below-minimum fails, maximum length is accepted without timeout.

## Pass/Fail Criteria

**Pass:**
- Exactly-at-minimum length passes validation
- Below-minimum length fails with CRITICAL
- Maximum length content validated without timeout/truncation

**Fail:**
- Boundary conditions handled incorrectly
- Timeout or truncation at maximum length
