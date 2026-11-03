---
id: ELITEA-4282
title: "Verify Preview mode never displays the Skill frontmatter block"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An existing Skill is available; Chat canvas Skill editor is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Skill, switch Instructions to Edit mode | Frontmatter is visible at the top of the editor |
| 2 | Switch to Preview mode | Rendered output shows only the body content; no `---`-delimited frontmatter block is visible |
| 3 | Edit the frontmatter `name`/`description` values in Edit mode (without saving), then switch to Preview mode | Frontmatter remains hidden regardless of the pending edit |
| 4 | Repeat steps 1–2 for a Skill opened via the Chat canvas Skill editor | Same Preview-mode behavior is observed (frontmatter hidden) |

## Expected Final State

Preview mode consistently renders only the Skill body across all entry points, never the frontmatter.

## Pass/Fail Criteria

**Pass:**
- Frontmatter is hidden in Preview mode in every tested scenario, including with unsaved edits and via the Chat canvas editor

**Fail:**
- Frontmatter appears in Preview mode under any tested scenario
