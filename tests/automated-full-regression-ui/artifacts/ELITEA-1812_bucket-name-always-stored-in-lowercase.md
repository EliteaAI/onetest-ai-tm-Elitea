---
id: ELITEA-1812
title: "Bucket Name Field: Validation Rules (empty, lowercase, length limits, save/cancel)"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1812: Bucket Name Field: Validation Rules (empty, lowercase, length limits, save/cancel)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify comprehensive bucket name field validation: empty name validation, lowercase conversion, character length limits (55, 56, 57 chars), and Save/Cancel button behavior.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Empty validation message | Name is required |
| Uppercase test name | BUCKET-TEST |
| Expected lowercase name | bucket-test |
| 55-character name | bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x |
| 56-character name | bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5 |
| Extra character (57th) | z |

---

## Steps

### Part 1: Empty Name Validation and Cancel Button

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/create icon above the bucket list | "New Bucket" form opens |
| 3 | Delete the default "new-bucket" name from the Name field | Name field is empty |
| 4 | Verify Save button is disabled | Save button appears disabled |
| 5 | Verify inline validation message "Name is required" is displayed | Validation message is visible |
| 6 | Verify Cancel button is active | Cancel button is enabled |
| 7 | Click Cancel button | Form closes |
| 8 | Verify no bucket was created | Bucket list unchanged |

### Part 2: Lowercase Conversion

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Click the folder/create icon again | "New Bucket" form opens |
| 10 | Enter uppercase name: "BUCKET-TEST" | Name field accepts input |
| 11 | Click Save | Bucket is created |
| 12 | Navigate back to Artifacts root | Artifacts page displays |
| 13 | Verify bucket appears as "bucket-test" (lowercase) in bucket list | Bucket name is all lowercase |

### Part 3: 55-Character Name

| # | Action | Expected Result |
|---|--------|-----------------|
| 14 | Click the folder/create icon | "New Bucket" form opens |
| 15 | Enter 55-character name: "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x" | Name field accepts all 55 characters |
| 16 | Verify character counter shows some characters remaining (not at limit) | Counter shows remaining characters |
| 17 | Click Save | Bucket is created successfully |
| 18 | Verify 55-char bucket appears in list | Bucket is visible with full 55-char name |
| 19 | Delete the 55-char bucket via its 3-dot menu → Delete | Bucket is deleted |

### Part 4: 56-Character Limit (Maximum Allowed)

| # | Action | Expected Result |
|---|--------|-----------------|
| 20 | Click the folder/create icon | "New Bucket" form opens |
| 21 | Enter 56-character name: "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5" | Name field accepts all 56 characters |
| 22 | Verify character limit warning shows "0 of 56 remaining" | Warning displays "0 of 56 remaining" |
| 23 | Click Save | Bucket is created successfully |
| 24 | Verify 56-char bucket appears in list | Bucket is visible with full 56-char name |
| 25 | Delete the 56-char bucket | Bucket is deleted |

### Part 5: Hard 56-Character Limit Enforcement (57th Character Rejected)

| # | Action | Expected Result |
|---|--------|-----------------|
| 26 | Click the folder/create icon | "New Bucket" form opens |
| 27 | Enter 56-character name again | All 56 characters accepted |
| 28 | Verify character limit warning shows "0 of 56 remaining" | Warning shows "0 of 56 remaining" |
| 29 | Attempt to type additional character "z" (making it 57 chars) | Character "z" is NOT accepted |
| 30 | Verify Name field still contains exactly 56 characters (no 57th) | Field has exactly 56 characters |
| 31 | Verify character limit warning still shows "0 of 56 remaining" | Warning unchanged at "0 of 56 remaining" |
| 32 | Click Cancel to close form without creating bucket | Form closes |

---

## Expected Final State

- Empty name prevents Save and shows validation message; Cancel works correctly
- Uppercase names are automatically converted to lowercase
- 55-character names are accepted and saved
- 56-character names are accepted (hard limit) with warning
- 57th character attempt is rejected; field enforces 56-char maximum

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Empty validation works; Cancel closes form without creating bucket.
- Uppercase converts to lowercase.
- 55-char and 56-char names save successfully.
- 57th character is rejected; field stays at 56 chars.

**Fail:**
- Any step produces an error or unexpected result.
- Validation does not work correctly, or character limits are not enforced.

---

## Notes

**Source functional tests:** ELITEA-1812, ELITEA-1813, ELITEA-1815, ELITEA-1817, ELITEA-1818, ELITEA-1819

**Regression rationale:** Consolidates bucket name field validation rules into a comprehensive test covering all validation behaviors: required field, case conversion, length limits, and button states.

**Selected checkpoints:**
- Empty name validation and Save button disabled state (ELITEA-1813)
- Cancel button functionality (ELITEA-1815)
- Uppercase to lowercase conversion (ELITEA-1812)
- 55-character name acceptance (ELITEA-1817)
- 56-character maximum with warning (ELITEA-1818)
- Hard 56-character limit enforcement (ELITEA-1819)
