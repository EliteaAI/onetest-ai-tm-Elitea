---
id: ELITEA-4278
title: "Verify editing Name/Description fields updates the frontmatter immediately, including block insertion and broken YAML handling"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role, editing an existing Skill with a valid frontmatter block present

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| New Name | `fields-to-editor-test` |
| New Description | `Testing fields-to-editor sync` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Edit the Name field to a new value | Only the `name:` line in the frontmatter is rewritten; the `description:` line and body text remain unchanged |
| 2 | Edit the Description field to a new value | Only the `description:` line is rewritten; other lines remain unchanged |
| 3 | Delete the entire frontmatter block from the editor, then edit the Name or Description field | A new frontmatter block is inserted at the top of the editor containing the current Name and Description |
| 4 | Introduce broken YAML in the frontmatter (unclosed quote), then edit the Name or Description field | Editor text is left untouched (not rewritten) while the YAML remains broken |

## Expected Final State

Field edits always propagate into the frontmatter text with minimal, targeted rewrites, except when the frontmatter is currently broken, in which case the editor text is never auto-modified.

## Pass/Fail Criteria

**Pass:**
- Only the edited key's line changes in the frontmatter; unrelated lines are untouched
- A missing frontmatter block is reinserted at the top when a field is edited
- Broken YAML is never rewritten by a field edit

**Fail:**
- Unrelated frontmatter lines change when only one field is edited
- No frontmatter block is inserted after deletion + field edit
- Broken YAML text is altered by a field edit
