---
id: ELITEA-1867
title: "Artifact Toolkit Creation – Negative Paths (Duplicate Bucket Name Fails, Cancel Creates Nothing)"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1867: Artifact Toolkit Creation – Negative Paths (Duplicate Bucket Name Fails, Cancel Creates Nothing)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify two negative paths of Artifact Toolkit creation: attempting to create a toolkit with a bucket name that already exists results in an error and nothing is saved, and clicking Cancel while filling in the form creates neither a toolkit nor a bucket.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket named "new-bucket" already exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing bucket name | new-bucket |
| New toolkit name (duplicate test) | my-duplicate-toolkit |
| Error notification | Bucket with name new-bucket already exists |
| Toolkit name (cancel test) | cancelled-toolkit |
| Bucket name (cancel test) | cancelled-bucket |

---

## Steps

### Part 1: Duplicate Bucket Name Is Rejected

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and verify a bucket named "new-bucket" already exists in the bucket list | "new-bucket" is listed |
| 2 | Navigate to the Toolkits section in the left sidebar | Toolkits page loads |
| 3 | Click the "+ Toolkit" button | "New Toolkit" page opens |
| 4 | Verify the "New Toolkit" page opens with the "Choose the toolkit type" heading | Page title is correct |
| 5 | Type "art" in the search field | Only "Artifact" toolkit shown |
| 6 | Verify only the "Artifact" toolkit is displayed under "STORAGE" | Filter works correctly |
| 7 | Click on the "Artifact" toolkit card | "New Artifact Toolkit" form opens |
| 8 | Verify the "New Artifact Toolkit" configuration form opens | Form is visible |
| 9 | In the "Toolkit Name *" field enter: "my-duplicate-toolkit" | Name field shows "my-duplicate-toolkit" |
| 10 | In the "Bucket *" field enter: "new-bucket" | Bucket field shows "new-bucket" |
| 11 | Click the "Save" button | Save is attempted |
| 12 | Verify an error notification is displayed indicating the bucket with name "new-bucket" already exists | Error notification appears |
| 13 | Verify the toolkit creation form remains open and the toolkit is NOT saved | Form is still visible |
| 14 | Verify the page URL remains on the create toolkit page | URL is unchanged |
| 15 | Navigate to the Toolkits section and verify no new toolkit named "my-duplicate-toolkit" appears in the toolkit list | "my-duplicate-toolkit" is not in the list |
| 16 | Navigate to the Artifacts section and search for "new-bucket" in the bucket search field | Search is performed |
| 17 | Verify only one "new-bucket" entry exists in the filtered results (no duplicate was created) | Exactly one "new-bucket" entry is present |

### Part 2: Cancel During Creation Creates Nothing

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | Navigate to the Toolkits section in the left sidebar | Toolkits list page is displayed |
| 19 | Click the "+ Toolkit" button | "New Toolkit" page opens |
| 20 | Type "art" in the search field and click on the "Artifact" toolkit card | "New Artifact Toolkit" form opens |
| 21 | In the "Toolkit Name *" field enter: "cancelled-toolkit" | Name field shows "cancelled-toolkit" |
| 22 | In the "Bucket *" field enter: "cancelled-bucket" | Bucket field shows "cancelled-bucket" |
| 23 | Verify both "Save" and "Cancel" buttons are visible and active in the top-right | Both buttons are present and active |
| 24 | Click the "Cancel" button | Form closes and page navigates to Toolkits list |
| 25 | Verify the form closes and the user is navigated back to the Toolkits list page | Toolkits list page is shown |
| 26 | Verify no toolkit named "cancelled-toolkit" appears in the toolkit list | "cancelled-toolkit" is absent |
| 27 | Navigate to the Artifacts section, search for "cancelled" | Bucket list filters |
| 28 | Verify no bucket named "cancelled-bucket" appears in the filtered results | "cancelled-bucket" is absent; no bucket was created |

---

## Expected Final State

Neither negative path creates unwanted state: the duplicate-bucket-name attempt leaves exactly one "new-bucket" and no "my-duplicate-toolkit"; the cancelled creation leaves no "cancelled-toolkit" and no "cancelled-bucket".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Duplicate bucket name is rejected with an error, form stays open, no duplicate toolkit/bucket created.
- Cancel returns to the Toolkits list with no toolkit or bucket created.

**Fail:**
- Any step produces an error or unexpected result.
- A toolkit or bucket is created with a duplicate name, or after Cancel.

---

## Notes

**Source functional tests:** ELITEA-1867, ELITEA-1868

**Regression rationale:** Both tests are negative paths of the same Artifact Toolkit creation flow (reject-on-duplicate-name and abort-on-cancel); consolidating into one test with two parts avoids duplicated toolkit-creation-form setup while preserving both checkpoints, mirroring the consolidation pattern already used for ELITEA-1844's delete-flow negatives.

**Selected checkpoints:**
- Duplicate bucket name blocks toolkit save with error, no duplicate created (ELITEA-1867)
- Cancel during creation returns to Toolkits list with nothing created (ELITEA-1868)
