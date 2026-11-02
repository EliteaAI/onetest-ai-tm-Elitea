---
id: ELITEA-4275
title: "Verify Save stores Name and Description from fields only, excluding frontmatter from the Skill body"
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
- An existing Skill is available for editing

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| New Name | `updated-skill-name` |
| New Description | `Updated skill description for save test` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Skill in Edit mode | Skill detail page loads with Instructions editor showing frontmatter and body |
| 2 | Edit the Name and Description fields directly (not via frontmatter) to the test data values above | Fields accept and display the new values |
| 3 | Click Save | Save completes without error; Save/Discard controls return to disabled state |
| 4 | Reopen the Skill | Name and Description fields show the values entered in step 2 |
| 5 | Inspect the raw stored Instructions value via Preview mode, an exported `.md` file, or the API response | No `---` frontmatter block is present in the raw stored Instructions value |
| 6 | Delete the frontmatter block entirely in the Instructions editor (leave body intact) and click Save | Save is not blocked; Name/Description are saved from the fields; body text is saved correctly; raw-storage check shows no frontmatter block |
| 7 | Reopen the Skill, introduce broken YAML in the frontmatter (e.g. unclosed quote on the name line), and click Save | Save is not blocked; Name/Description are saved from the fields; body text after the frontmatter region is saved correctly; raw-storage check shows no frontmatter block |

## Expected Final State

The Skill's Name and Description are persisted exactly as entered in the form fields; the stored Instructions/body never contains a frontmatter block, regardless of what was present or broken in the editor's frontmatter text at Save time. Note: reopening the Skill in Edit mode regenerates a fresh frontmatter block for display — this is expected and is not evidence of persisted frontmatter.

## Pass/Fail Criteria

**Pass:**
- Name/Description persisted match field values after Save
- Raw stored Instructions (Preview/export/API) never contains a `---` frontmatter block, across the normal, deleted-frontmatter, and broken-YAML scenarios
- Save is not blocked by a deleted or broken frontmatter block

**Fail:**
- Raw stored Instructions contains a frontmatter block
- Save is blocked or errors due to frontmatter state
- Saved Name/Description do not match the field values
