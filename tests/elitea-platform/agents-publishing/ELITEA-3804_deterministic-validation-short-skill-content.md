---
id: ELITEA-3804
title: "Deterministic validation - short skill content"
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
- Test agent created with valid base configuration
- Skill prepared with short content (below minimum length threshold)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill Name | "Short Skill" |
| Skill Content | Instructions: "Do this." (< 100 chars, below minimum length) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attach "Short Skill" to test agent | Skill attached |
| 2 | Click ⋮ menu → **Publish** | Wizard opens |
| 3 | Complete Preparation step | Continue to Validation |
| 4 | Wait for validation | Result: **FAIL** (red summary with a short description of the problem) |
| 5 | Verify CRITICAL finding | Finding: Minimum length violation |
| 6 | Verify finding context | Context shows: `skill: Short Skill` |
| 7 | Verify **Publish** button state | Button **disabled** |
| 8 | Cancel wizard | Return to agent |
| 9 | Edit "Short Skill" to add more content (100+ chars) | Skill content now meets minimum length |
| 10 | Repeat publish flow to Validation | Wait for results |
| 11 | Verify no length violation | No CRITICAL finding for length |
| 12 | Verify **Publish** button state | Button **enabled** (if no other criticals) |

## Expected Final State

Validation correctly identifies below-minimum length Skill content as CRITICAL and blocks publishing. After fixing content length, validation passes and publishing is enabled.

## Pass/Fail Criteria

**Pass:**
- Below-minimum length instructions → CRITICAL length violation
- CRITICAL finding correctly attributed to specific Skill name
- Publish button disabled while CRITICAL exists
- After fixing content length, validation passes

**Fail:**
- Short content not detected as CRITICAL
- Finding not attributed to correct Skill
- Publish button enabled despite CRITICAL
- Validation still fails after fixing content
