---
id: ELITEA-1868
title: "Cancel During Artifact Toolkit Creation Does Not Create Toolkit or Bucket"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1868: Cancel During Artifact Toolkit Creation Does Not Create Toolkit or Bucket

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel while filling in the Artifact Toolkit creation form navigates back to the Toolkits list without creating a toolkit or a bucket.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit name (to enter) | cancelled-toolkit |
| Bucket name (to enter) | cancelled-bucket |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Toolkits section in the left sidebar | Toolkits list page is displayed |
| 2 | Click the "+ Toolkit" button | "New Toolkit" page opens |
| 3 | Verify the "New Toolkit" page opens with the "Choose the toolkit type" heading | Page title is correct |
| 4 | Type "art" in the search field | Only "Artifact" toolkit shown |
| 5 | Verify only the "Artifact" toolkit is displayed under "STORAGE" | Filter works correctly |
| 6 | Click on the "Artifact" toolkit card | "New Artifact Toolkit" form opens |
| 7 | Verify the "New Artifact Toolkit" configuration form opens | Form is visible |
| 8 | In the "Toolkit Name *" field enter: "cancelled-toolkit" | Name field shows "cancelled-toolkit" |
| 9 | In the "Bucket *" field enter: "cancelled-bucket" | Bucket field shows "cancelled-bucket" |
| 10 | Verify both "Save" and "Cancel" buttons are visible and active in the top-right | Both buttons are present and active |
| 11 | Click the "Cancel" button | Form closes and page navigates to Toolkits list |
| 12 | Verify the form closes and the user is navigated back to the Toolkits list page | Toolkits list page is shown |
| 13 | Verify no toolkit named "cancelled-toolkit" appears in the toolkit list | "cancelled-toolkit" is absent |
| 14 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 15 | Click the search icon in the "BUCKETS" header | Search field opens |
| 16 | Type "cancelled" in the search field | Bucket list filters |
| 17 | Verify no bucket named "cancelled-bucket" appears in the filtered results | "cancelled-bucket" is absent |
| 18 | Verify the bucket was not created as a result of the cancelled toolkit creation | No bucket created |

---

## Expected Final State

No toolkit named "cancelled-toolkit" and no bucket named "cancelled-bucket" were created. The user is returned to the Toolkits list after clicking Cancel.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No toolkit or bucket created after Cancel; user returned to Toolkits list.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit or bucket is created after Cancel.
