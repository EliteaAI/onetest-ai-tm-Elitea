---
id: ELITEA-4287
title: "Verify a deleted frontmatter block does not block Save and is regenerated correctly on reopen"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role, editing an existing Skill

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Skill and delete the entire frontmatter block (including both `---` delimiters) from the Instructions editor, leaving only the body text | Editor shows only the body text, no frontmatter |
| 2 | Click Save | No error occurs; Save succeeds using the current Name/Description field values and the remaining editor content as the body |
| 3 | Reopen the Skill | A frontmatter block is regenerated at the top of the editor, populated from the saved Name/Description |

## Expected Final State

Deleting the frontmatter block entirely is a benign, recoverable state — Save still works, and the frontmatter reappears correctly on next open.

## Pass/Fail Criteria

**Pass:**
- Save succeeds with the frontmatter block absent
- Frontmatter is correctly regenerated on reopen, matching saved Name/Description

**Fail:**
- Save is blocked or errors when the frontmatter block is absent
- Frontmatter is missing, incorrect, or stale on reopen
