---
id: ELITEA-1866
title: "Create Artifact Bucket via Artifact Toolkit Creation and Verify via List Files Tool"
priority: high
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id: tests.ui.toolkits.test_toolkit_creation_create_bucket_verify_list_files.TestToolkitCreationCreateBucketVerifyListFiles.test_create_artifact_toolkit_creates_bucket_verify_list_files
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2080
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1866: Create Artifact Bucket via Artifact Toolkit Creation and Verify via List Files Tool

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify the end-to-end flow of creating an Artifact Toolkit (which also creates a bucket), verifying all UI elements of the toolkit creation form, running the "List files" tool in the test panel, and confirming the new bucket exists in the Artifacts section.

---

## Preconditions

- User is logged in to the Elitea platform.
- No existing bucket or toolkit named "new-bucket" or "my-artifact-toolkit".

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit name | my-artifact-toolkit |
| Bucket name | new-bucket |
| Search term | art |
| Toolkit type | Artifact (under STORAGE) |
| Tool to test | List files |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Toolkits section in the left sidebar | Toolkits list page is displayed |
| 2 | Verify the Toolkits list page is displayed showing all existing toolkits with their types | Toolkits list is visible |
| 3 | Click the "+ Toolkit" button in the top-left area | "New Toolkit" page opens |
| 4 | Verify the "New Toolkit" page opens with the heading "Choose the toolkit type" | Page title is correct |
| 5 | Verify a search input field is present with placeholder text "Search toolkits" | Search field is visible |
| 6 | Verify category filter tabs are displayed | All category tabs are present |
| 7 | Type "art" in the search field | Toolkit list filters |
| 8 | Verify the toolkit list filters and shows only the "Artifact" toolkit under the "STORAGE" section | Only Artifact toolkit is shown |
| 9 | Verify no other toolkit types are displayed | No other toolkits visible |
| 10 | Click on the "Artifact" toolkit card | "New Artifact Toolkit" configuration form opens |
| 11 | Verify the form opens with "Form" and "Raw Json" tabs, "CONFIGURATION" section with Toolkit Name, Description, Pgvector Configuration, Embedding Model, and Bucket fields | All configuration fields are present |
| 12 | Verify the "TOOLS" section shows all 16 available tools with checkmarks | All tools listed with checkmarks |
| 13 | Verify a "Make tools available by MCP" checkbox (unchecked by default) | MCP checkbox is present and unchecked |
| 14 | Verify "Save" and "Cancel" buttons in the top-right | Both buttons are present |
| 15 | Click the info (i) icon next to the "Bucket *" field | Tooltip appears with bucket name rules |
| 16 | Verify the tooltip displays the bucket naming rules (start with lowercase letter, only lowercase letters/numbers/hyphens, unique within project) | Correct tooltip content is shown |
| 17 | In the "Toolkit Name *" field enter: "my-artifact-toolkit" | Name field shows "my-artifact-toolkit" |
| 18 | In the "Bucket *" field enter: "new-bucket" | Bucket field shows "new-bucket" |
| 19 | Leave all other fields at their default values | Defaults are retained |
| 20 | Click the "Save" button | Toolkit is saved and page navigates to detail view |
| 21 | Verify the page navigates to the toolkit detail/configuration view | Detail view is shown |
| 22 | Verify the page header displays the toolkit name (or "new-bucket") | Correct name is shown |
| 23 | Verify the URL updates to reflect the new toolkit | URL contains toolkit ID |
| 24 | Verify "Configuration" and "Indexes" tabs are shown at the top | Both tabs are present |
| 25 | Verify the "TEST SETTINGS" panel is visible on the right side with model selector, Tool dropdown, and welcome message | Test settings panel is visible with all elements |
| 26 | In the "TEST SETTINGS" panel click the "Tool" dropdown | Tool list expands |
| 27 | Verify the tool list shows all available tools including "List files" | All tools including "List files" are listed |
| 28 | Select "List files" from the tool dropdown | "List files" parameters panel appears |
| 29 | Verify the "List files" tool parameters panel shows: Bucket Name, Folder, Recursive checkbox, Include array, Skip array, and "RUN TOOL" button | All parameters and button are present |
| 30 | Click the "RUN TOOL" button | Tool runs and returns a result |
| 31 | Verify the tool runs and returns a result in the center chat/output panel | Result is displayed |
| 32 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 33 | Click the search icon in the "BUCKETS" header | Search field opens |
| 34 | Type "new" in the search field | Bucket list filters |
| 35 | Verify the bucket list filters and displays buckets containing "new" | Filtered list is shown |
| 36 | Verify "new-bucket" is listed in the filtered results | "new-bucket" is present |
| 37 | Click on "new-bucket" to select it | "new-bucket" is selected |
| 38 | Verify the main panel header displays "new-bucket" | Header shows "new-bucket" |
| 39 | Verify the main panel shows "No files in this bucket" with an "Upload files" button | Empty bucket state is shown |

---

## Expected Final State

An Artifact Toolkit "my-artifact-toolkit" is created which also creates bucket "new-bucket". The toolkit test panel works with the "List files" tool. The "new-bucket" is visible and empty in the Artifacts section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit created; bucket exists; List files tool runs; bucket visible in Artifacts section.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit not saved, bucket not created, or tool does not run.
