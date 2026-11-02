---
id: ELITEA-4276
title: "Verify frontmatter is generated correctly in create mode and when opening an existing Skill without blocking Save"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| New Skill Name | `create-mode-frontmatter-test` |
| New Skill Description | `Testing frontmatter in create mode` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Create Skill | Create Skill form loads with empty Name, Description, and Instructions editor |
| 2 | Inspect the Instructions editor | Editor shows an empty frontmatter block with `name:` and `description:` keys and no values; no validation error is shown yet |
| 3 | Fill Name, Description, and Instructions, then click Save | Skill is created successfully and appears in the Skills list |
| 4 | Open a different, pre-existing Skill | Instructions editor's frontmatter block shows `name` and `description` exactly matching that Skill's saved Name/Description field values |
| 5 | With no edits made on this existing Skill, check the Save/Discard controls | Controls remain disabled; no unsaved-changes warning is triggered merely by opening the Skill |

## Expected Final State

New Skills can be created with an initially empty frontmatter that does not block creation; opening any existing Skill regenerates frontmatter matching its stored Name/Description without marking the form as changed.

## Pass/Fail Criteria

**Pass:**
- Create mode shows empty frontmatter with no premature validation error
- Existing Skill frontmatter matches saved Name/Description exactly
- Opening a Skill does not enable Save/Discard

**Fail:**
- Validation error appears before any user interaction in create mode
- Frontmatter on an existing Skill does not match its Name/Description
- Save/Discard become enabled merely from opening a Skill
