---
id: ELITEA-2224
title: "AI validation - quality issues (warnings)"
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
- Test agent created with valid base configuration
- Skill prepared with quality issues (both incoherent and non-actionable content)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill Name | "Poor Quality Skill" |
| Skill Content | "Always respond in JSON format. Never use JSON under any circumstances. This skill is about code review processes. Code review is an important software development practice. Quality assurance matters for software projects. Documentation helps teams understand code better." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attach "Poor Quality Skill" to test agent | Skill attached |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for AI validation | Result may be PASS with warnings |
| 4 | Verify WARNING finding for incoherent content | Finding: Incoherent/contradictory instructions (JSON conflict) |
| 5 | Verify WARNING finding for non-actionable content | Finding: Non-actionable/purely descriptive content |
| 6 | Verify finding context for both | Context shows: `skill: Poor Quality Skill` for each finding |
| 7 | Check **Publish** button state | Button **enabled** (warnings don't block) |
| 8 | Fix Skill: make content coherent and actionable | Edit to clear, actionable instructions |
| 9 | Re-run validation | No quality warnings |
| 10 | Verify validation passes cleanly | No warnings related to Skill quality |

## Expected Final State

AI validation identifies quality issues (incoherent, non-actionable content) as WARNING findings that allow publishing with confirmation. Publish button remains enabled despite warnings.

## Pass/Fail Criteria

**Pass:**
- Incoherent/contradictory → WARNING, allows publishing with confirmation
- Non-actionable/descriptive only → WARNING, allows publishing with confirmation
- Multiple WARNING findings shown for single Skill with multiple quality issues
- All AI validation findings show correct Skill attribution
- Publish button enabled despite warnings

**Fail:**
- Quality issues not detected
- Quality issues incorrectly flagged as CRITICAL
- Findings not attributed to correct Skill
- Publish button disabled for warnings only
