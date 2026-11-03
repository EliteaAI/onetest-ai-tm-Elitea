---
id: ELITEA-4283
title: "Verify Edit-with-AI wizard and Generate Skill review form never display frontmatter"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Admin or Editor role
- An existing Skill is available for Edit-with-AI

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Edit Prompt | `Make this skill more detailed and professional` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Skill and trigger "Edit with AI" | Edit with AI wizard opens |
| 2 | Step through to the Instructions comparison step (Current vs Suggested) | Neither Current nor Suggested Instructions display a frontmatter block |
| 3 | Proceed to the Summary step | No frontmatter is shown there either |
| 4 | Trigger the Generate Skill flow (AI-generated draft) and open its review form | Instructions preview shows body content only, with no frontmatter block |
| 5 | Re-validate ELITEA-2611-merged end-to-end | Overall Edit-with-AI workflow (visibility by role, wizard steps, diff highlighting, character-limit enforcement) still functions correctly with frontmatter present in the base editor |

## Expected Final State

The AI-assisted editing and generation flows remain unaffected by the frontmatter feature — they continue to operate on body-only content, as declared out-of-scope by the issue.

## Pass/Fail Criteria

**Pass:**
- No frontmatter is ever shown in the Edit-with-AI wizard or Generate Skill review form
- Existing Edit-with-AI regression coverage (ELITEA-2611-merged) still passes

**Fail:**
- Frontmatter appears anywhere in the Edit-with-AI wizard or Generate Skill review form
- Any regression in ELITEA-2611-merged behavior
