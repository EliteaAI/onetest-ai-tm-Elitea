---
id: ELITEA-4281
title: "Verify a missing closing --- line blocks body updates and Save preserves the previous body"
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
- An existing Skill with known Instructions content is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| New (should-not-persist) body text | `This text should not be saved` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Skill with known Instructions content | Skill loads with known Instructions |
| 2 | In the Instructions editor, delete the closing `---` line of the frontmatter block | Closing delimiter is removed from the editor text |
| 3 | Type new text in what would be the body area | Text is typed into the editor (visually present) |
| 4 | Click Save | Save completes without error |
| 5 | Reopen the Skill | Instructions content matches the previously saved body (the in-progress body edit from step 3 was not persisted); a frontmatter block is regenerated from the current Name/Description |

## Expected Final State

While the closing `---` is missing, body edits are not recognized by the form; a Save in that state does not corrupt the stored Instructions — it retains the last known-good body.

## Pass/Fail Criteria

**Pass:**
- Body text typed while the closing `---` is missing is not saved
- Previously saved body is intact after Save + reopen
- Frontmatter regenerates correctly on reopen

**Fail:**
- The in-progress body edit is saved despite the missing closing `---`
- Previously saved body is lost or corrupted
