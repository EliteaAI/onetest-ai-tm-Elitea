---
id: ELITEA-1819
title: "Bucket Name Field Does Not Accept More Than 56 Characters"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1819: Bucket Name Field Does Not Accept More Than 56 Characters

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the bucket Name field enforces a maximum of 56 characters by rejecting any additional character input once the limit is reached.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| 56-character name | bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5 |
| Extra character | z |
| Character limit indicator | 0 of 56 remaining |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 3 | Verify the "New Bucket" form opens | Form is visible |
| 4 | Enter the 56-character bucket name: "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5" | Name field accepts all 56 characters |
| 5 | Verify the character limit warning is displayed indicating "0 of 56 remaining" | Warning shows "0 of 56 remaining" |
| 6 | Attempt to type one additional character (e.g., "z") to make the name 57 characters long | Attempt to add extra character |
| 7 | Verify the additional character is not accepted and the Name field still contains exactly 56 characters | Field still contains exactly 56 characters; "z" is not added |
| 8 | Verify the character limit warning still shows "0 of 56 remaining" | Warning still shows "0 of 56 remaining" |
| 9 | Verify the bucket name has not changed in the Name field | Name field content is unchanged |

---

## Expected Final State

The Name field enforces a hard maximum of 56 characters. Any attempt to type a 57th character is rejected and the field content remains at exactly 56 characters.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The 57th character is rejected and the field remains at 56 characters.

**Fail:**
- Any step produces an error or unexpected result.
- More than 56 characters are accepted in the Name field.
