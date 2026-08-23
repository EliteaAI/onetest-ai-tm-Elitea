---
id: ELITEA-1812
title: "Bucket Name Is Always Stored and Displayed in Lowercase"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_bucket_name_lowercase.TestArtifactBucketNameLowercase.test_uppercase_bucket_name_is_stored_and_displayed_lowercase
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1686
requirements: []
---

# ELITEA-1812: Bucket Name Is Always Stored and Displayed in Lowercase

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that when a bucket name is entered in uppercase, it is automatically stored and displayed in lowercase in the bucket list.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Input bucket name | BUCKET-TEST |
| Expected stored name | bucket-test |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/create icon located above the bucket list | "New Bucket" form opens |
| 3 | Enter bucket name in uppercase: "BUCKET-TEST" | Name field accepts the input |
| 4 | Click "Save" | Bucket is saved |
| 5 | Click to "Artifacts" | Navigation to Artifacts root occurs |
| 6 | Verify the bucket appears in the bucket list as "bucket-test" (all lowercase) | Bucket is listed as "bucket-test" in lowercase |

---

## Expected Final State

The bucket "BUCKET-TEST" is created and displayed as "bucket-test" in the bucket list, confirming automatic lowercase conversion.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Bucket name is stored and displayed in all lowercase regardless of input case.

**Fail:**
- Any step produces an error or unexpected result.
- Bucket name retains uppercase characters in the list.
