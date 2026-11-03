---
id: ELITEA-4277
title: "Verify editing frontmatter name and description syncs to Name/Description fields with correct freeze behavior on invalid input"
priority: critical
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

| Case | Frontmatter Input |
|------|--------------------|
| Valid name | `name: my-updated-skill` |
| Description with special chars | value containing `:`, `#`, a quote `"`, a leading `-`, and a line break |
| Renamed/partial key | `na: my-skill` or bare `na` |
| Empty value | `name:` with nothing after it |
| Broken YAML | `name: "my-skill` (unclosed quote) |
| Over-limit name | name value exceeding 64 characters |
| Over-limit description | description value exceeding the Description field's character limit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Edit the `name:` value in the frontmatter to a new valid value (e.g. `my-updated-skill`) | Name field updates immediately to match |
| 2 | Edit the `description:` value in the frontmatter to a value containing `:`, `#`, a quote, a leading `-`, and a line break | Description field updates immediately; round-tripped value matches exactly with no extra characters (e.g. no trailing newline) |
| 3 | Rename the `name` key (e.g. `na: my-skill`) or make it a partial/non-key-value line (e.g. `na`) | Name field keeps its last value and does not update |
| 4 | Clear the value after `name:` so it reads `name:` with nothing after it | Name field keeps its last value |
| 5 | Break the YAML with an unclosed quote (e.g. `name: "my-skill`) | Both Name and Description fields freeze at their last values |
| 6 | With YAML still broken from step 5, fix only the `description` line while leaving `name` broken | Description field updates independently while Name field remains frozen |
| 7 | Delete the entire frontmatter block from the editor | Both Name and Description fields keep their last values; no error shown |
| 8 | Enter a frontmatter `name` violating Skill naming rules (uppercase letters, disallowed characters, over 64 characters, or containing "claude"/"anthropic") | Invalid value is copied to the Name field; Name field's usual validation error is shown |
| 9 | Enter a frontmatter `description` exceeding the Description field's character limit | Value is copied to the Description field; Description field's usual validation error is shown |
| 10 | Throughout steps 3–7, check for frontmatter-specific warnings | No frontmatter-specific warning or error message is ever displayed in the editor itself |
| 11 | Edit the frontmatter `name` value to exceed 64 characters | Name field immediately syncs to show the over-limit value; validation error is displayed; Save is disabled/blocked while the error is present |
| 12 | Edit the frontmatter `description` value to exceed the Description field's character limit | Description field immediately syncs to show the over-limit value; validation error is displayed; Save is disabled/blocked while the error is present |
| 13 | Correct the over-limit value back to within the limit (via either the field or the frontmatter) | Validation error clears; Save becomes enabled again |

## Expected Final State

Name/Description fields reflect only validly-parsed, non-empty frontmatter keys; any over-limit or malformed value is surfaced through the Name/Description field's own validation and blocks Save; no frontmatter-specific error UI exists anywhere in the editor.

## Pass/Fail Criteria

**Pass:**
- Fields update only under the documented valid-parse conditions; otherwise retain last value
- Broken YAML freezes both fields; each key is otherwise evaluated independently
- Over-limit values surface the field's own validation error and block Save
- No frontmatter-specific error messaging appears

**Fail:**
- A field updates despite missing/invalid/empty key, or fails to update despite valid input
- Broken YAML only freezes one field
- Over-limit frontmatter input does not block Save or does not show the field's error
- A frontmatter-specific warning/error is shown
