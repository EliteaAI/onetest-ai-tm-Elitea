---
id: ELITEA-1867
title: "Artifact Toolkit Creation Fails When Bucket Name Already Exists"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1867: Artifact Toolkit Creation Fails When Bucket Name Already Exists

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that attempting to create an Artifact Toolkit with a bucket name that already exists results in an error notification, the form remains open, and no duplicate toolkit or bucket is created.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket named "new-bucket" already exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing bucket name | new-bucket |
| New toolkit name | my-duplicate-toolkit |
| Error notification | Bucket with name new-bucket already exists |

---

## Steps

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

---

## Expected Final State

No toolkit named "my-duplicate-toolkit" is created and no duplicate "new-bucket" is created. The error notification is displayed and the form remains open.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Error notification shown; form remains open; no duplicate toolkit or bucket created.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit is saved with a duplicate bucket name, or error notification is not displayed.
