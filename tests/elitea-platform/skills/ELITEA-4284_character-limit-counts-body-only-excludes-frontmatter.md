---
id: ELITEA-4284
title: "Verify the Skill content character limit counts body only, excluding frontmatter length"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role, editing a Skill

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Long description (within field limit) | Several hundred characters |
| Body text | Text filled up to just below the Instructions character limit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Skill and note the "characters left" counter shown near the Instructions editor | Counter displays current remaining character count for the body |
| 2 | Add a long `description` value in the frontmatter (several hundred characters, within the Description field's own limit) | Instructions "characters left" counter does not decrease because of the frontmatter content |
| 3 | Fill the body with text up to just below the character limit, then attempt to add more body text beyond the limit | Input is cut off at the limit regardless of frontmatter length |
| 4 | Save the Skill at this boundary | No save error occurs due to frontmatter length being incorrectly counted |

## Expected Final State

The Instructions character limit is enforced strictly against body content; frontmatter length never contributes to the count, in the editor or on Save.

## Pass/Fail Criteria

**Pass:**
- "Characters left" counter is unaffected by frontmatter length
- Body input cutoff happens exactly at the body limit
- Save succeeds at the boundary with no frontmatter-related error

**Fail:**
- Counter decreases due to frontmatter content
- Body input is cut off earlier/later than the true body limit
- Save fails due to frontmatter length being counted
