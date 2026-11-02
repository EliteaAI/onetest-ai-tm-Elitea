---
id: ELITEA-4280
title: "Verify pasting a full SKILL.md populates Name/Description and ignores unrecognized frontmatter keys"
priority: critical
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

| Frontmatter Key | Example Value |
|------------------|----------------|
| name | `pasted-skill-example` |
| description | `Skill pasted from a full SKILL.md file` |
| license | `MIT` |
| allowed-tools | `[Read, Write]` |
| tags | `[example, pasted]` |
| elitea_run_settings | `{model: auto}` |
| version | `1.0.0` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Prepare a SKILL.md file whose frontmatter includes `name`, `description`, and the additional keys listed in Test Data | File is ready for paste |
| 2 | Select all content in the Instructions editor and paste the full file content over it | Editor content is replaced with the pasted file content |
| 3 | Inspect the Name and Description fields | Fields are populated from the pasted `name`/`description` values |
| 4 | Inspect the Instructions body | Body text after the pasted frontmatter's closing `---` becomes the Instructions body |
| 5 | Check for any validation message, warning, or error regarding the unrecognized keys | No message is shown regarding `license`, `allowed-tools`, `tags`, `elitea_run_settings`, or `version` |
| 6 | Save the Skill, then reopen it | None of the unrecognized keys are persisted anywhere; the regenerated frontmatter only contains `name`/`description` |

## Expected Final State

Pasting a full SKILL.md correctly extracts only `name`/`description` into their fields, keeps the rest as body, and silently drops all other frontmatter keys with no trace after Save.

## Pass/Fail Criteria

**Pass:**
- Name/Description fields match the pasted values
- Body matches the pasted content after the frontmatter
- No warning/error for unrecognized keys
- Unrecognized keys are not persisted after Save + reopen

**Fail:**
- Name/Description not populated correctly from paste
- Unrecognized keys trigger a warning/error
- Unrecognized keys are persisted or reappear after Save + reopen
