---
id: ELITEA-3806
title: "Deterministic validation - placeholder and secrets detection"
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
- Skill prepared with both placeholder text and hardcoded secrets

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill Name | "Bad Skill" |
| Skill Content | "TODO: Complete this authentication guide. Use API key sk-abc123xyz to authenticate. Set password=admin123 for access. TBD: Add more details later." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attach "Bad Skill" to test agent | Skill attached |
| 2 | Click ⋮ menu → **Publish** | Wizard opens |
| 3 | Complete Preparation step | Validation runs |
| 4 | Wait for validation | Result: **FAIL** |
| 5 | Verify CRITICAL finding for placeholder | Finding mentions TODO/TBD/placeholder detection |
| 6 | Verify CRITICAL finding for secrets | Finding mentions inline secrets detected |
| 7 | Verify finding context for both | Context shows: `skill: Bad Skill` for each finding |
| 8 | Verify **Publish** button state | Button **disabled** |
| 9 | Fix Skill: remove placeholders and secrets | Edit to valid content (150+ chars, no issues) |
| 10 | Re-run validation | Result: **PASS** |
| 11 | Verify **Publish** button state | Button **enabled** |

## Expected Final State

Validation correctly identifies placeholder text and inline secrets in Skill content as CRITICAL findings. After removing both issues, validation passes.

## Pass/Fail Criteria

**Pass:**
- Placeholder text (TODO, TBD) → CRITICAL placeholder detection
- Inline secrets (sk-..., password=) → CRITICAL secrets detection
- Multiple CRITICAL findings shown for single Skill with multiple issues
- CRITICAL findings correctly attributed to Skill name
- Publish button disabled while CRITICAL exists
- After fixing, re-validation passes and Publish enabled

**Fail:**
- Placeholders or secrets not detected
- Findings not attributed to correct Skill
- Publish button enabled despite CRITICAL findings
