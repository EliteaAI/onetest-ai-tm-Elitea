---
id: ELITEA-1992
title: "Build with AI — Field Validation (Name, Description, Instructions)"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1992: Build with AI — Field Validation (Name, Description, Instructions)

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the Build with AI feature correctly validates the Name, Description, and Instructions fields: generated names follow naming rules, manual name edits are validated, and character limits are enforced for Description (2304 chars) and Instructions (50000 chars).

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The Build with AI modal is accessible from the New Skill creation screen.
- Platform is at the default "Skill Content Max Length" of 50000 characters.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "A skill that helps analyze code quality" |
| Invalid name (uppercase) | "MySkill" |
| Invalid name (spaces) | "my skill" |
| Invalid name (leading hyphen) | "-my-skill" |
| Invalid name (trailing hyphen) | "my-skill-" |
| Invalid name (exceeds 64 chars) | "this-is-a-very-long-skill-name-that-definitely-exceeds-the-sixty-four-character-limit-for-skill-names" |
| Over-limit description | A string of 2305 characters |
| Exact-limit description | A string of exactly 2304 characters |
| Exact-limit instructions | A string of exactly 50000 characters |
| Over-limit instructions paste | A string of 50001+ characters pasted in one paste |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Generated Name Validation** | | |
| 1 | Open the Build with AI modal and submit a prompt: "A skill that helps analyze code quality" | Generation is initiated and completes successfully |
| 2 | After generation, inspect the generated Name in the review form | The Name field is visible and populated |
| 3 | Verify the generated name contains only lowercase letters, digits, and hyphens | The generated name uses only allowed characters (lowercase, digits, hyphens) |
| 4 | Verify the generated name does not contain spaces, underscores, or special characters | No spaces, underscores, or special characters are present |
| 5 | Verify the generated name does not start or end with a hyphen | The first and last characters are not hyphens |
| 6 | Verify the generated name does not exceed 64 characters | The name length is 64 characters or fewer |
| **Manual Name Edit Validation** | | |
| 7 | Edit the Name field to a name with uppercase letters: "MySkill" | The "Create Skill" button is disabled or a validation error is shown |
| 8 | Edit the Name field to a name with spaces: "my skill" | The "Create Skill" button is disabled or a validation error is shown |
| 9 | Edit the Name field to a name starting with a hyphen: "-my-skill" | The "Create Skill" button is disabled or a validation error is shown |
| 10 | Edit the Name field to a name ending with a hyphen: "my-skill-" | The "Create Skill" button is disabled or a validation error is shown |
| 11 | Edit the Name field to a name exceeding 64 characters | The "Create Skill" button is disabled or a validation error is shown |
| 12 | Verify the user cannot create a Skill with any of the above invalid names | Attempting to submit with each invalid name is blocked by validation |
| **Description Character Limit** | | |
| 13 | Clear the Description field and paste a string of 2305 characters (exceeding 2304 limit) | The text is entered in the Description field |
| 14 | Verify a validation message is shown for the Description field | A validation error message is displayed for the Description field |
| 15 | Verify the "Create Skill" button is inactive/disabled | The "Create Skill" button is disabled or inactive |
| 16 | Trim the description to exactly 2304 characters | The Description field contains exactly 2304 characters |
| 17 | Verify the validation error clears and "Create Skill" becomes active | The validation error disappears and the "Create Skill" button becomes active |
| **Instructions Character Limit** | | |
| 18 | Clear the Instructions field and type or paste text past 50000 characters | Input is hard-blocked at exactly 50000 characters; no further characters can be typed or pasted |
| 19 | Paste a block of text that would take the field from under the limit to over 50000 characters in one paste | Pasted text is truncated to land exactly at 50000 characters; no error shown, no crash |
| 20 | With the Instructions field at exactly 50000 characters, verify the "Create Skill" button | "Create Skill" remains enabled |
| 21 | Verify no hardcoded "2500" character limit message or counter appears anywhere in the form | Only the configured limit (50000 by default) is referenced |

---

## Expected Final State

- Generated Skill names fully conform to naming rules: lowercase, digits, hyphens only; no leading/trailing hyphens; max 64 characters.
- Manual name edits are validated: invalid names (uppercase, spaces, leading/trailing hyphens, >64 chars) disable "Create Skill" or show validation errors.
- Description field enforces 2304-character limit with validation error when exceeded, cleared when trimmed to limit.
- Instructions field enforces 50000-character limit with hard input block; no stale 2500-character limit references.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified:
  - Generated name follows all naming rules
  - Each invalid manual name edit triggers validation error or disables "Create Skill"
  - Description validation error appears for >2304 chars, clears at ≤2304 chars
  - Instructions input hard-blocked at 50000 chars, no 2500-char limit references
  - "Create Skill" enabled for valid field values, disabled for invalid values

**Fail:**
- Any assertion fails:
  - Generated name violates naming rules
  - Form allows creating Skill with invalid name
  - Description accepts >2304 chars or incorrectly blocks ≤2304 chars
  - Instructions allows typing/pasting past 50000 chars, or shows stale 2500-char limit
  - "Create Skill" incorrectly enabled/disabled

---

## Notes

**Source functional tests:** ELITEA-1992, ELITEA-1993, ELITEA-1994, ELITEA-1995

**Regression rationale:** Consolidated from 4 tests to verify all field validations (name generation rules, name edit validation, description limit, instructions limit) in a single flow. This eliminates redundant draft generation steps while testing all validation rules systematically.

**Selected checkpoints:** Generated name compliance with rules, validation errors for each invalid name pattern, description character limit enforcement with error clearing, instructions hard-block at 50000 chars, "Create Skill" button state throughout validation scenarios.
