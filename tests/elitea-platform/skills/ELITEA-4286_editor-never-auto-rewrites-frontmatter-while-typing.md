---
id: ELITEA-4286
title: "Verify the frontmatter editor never auto-rewrites or repairs text while the user is typing"
priority: medium
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
| Malformed line example | `name: "unclosed` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Begin typing a new `name:` value character by character, pausing mid-value | Editor displays exactly what was typed at each pause; no automatic reformatting, quote insertion, or line restructuring |
| 2 | Type an intentionally malformed line (e.g. an unclosed quote) | Editor does not attempt to auto-close the quote or otherwise alter the raw text |

## Expected Final State

The frontmatter editor behaves as a plain text editor with no silent auto-correction, regardless of YAML validity.

## Pass/Fail Criteria

**Pass:**
- Typed text is shown exactly as entered at every step, valid or malformed

**Fail:**
- Editor auto-inserts, auto-closes, or reformats any character while typing
