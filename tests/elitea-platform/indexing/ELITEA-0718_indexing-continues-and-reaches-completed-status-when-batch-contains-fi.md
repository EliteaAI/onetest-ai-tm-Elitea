---
id: ELITEA-0718
title: "Indexing Continues and Reaches Completed Status When Batch Contains Files That Cannot Be Parsed [Parametrized]"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0718: Indexing Continues and Reaches Completed Status When Batch Contains Files That Cannot Be Parsed [Parametrized]

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that encountering an unparseable file does not stop the indexing job — it skips the problematic file, continues processing valid files, and ultimately reaches Completed status.

**Coverage:**
- Indexing does not stop at Failed when an unsupported-format file is in the bucket
- Indexing does not stop at Failed when a corrupted/truncated file is in the bucket
- Indexing does not stop at Failed when a password-protected PDF/XLSX is in the bucket
- Final status reaches ✅ Completed after all valid files are processed

## Preconditions

- Logged in to {{base_url}}
- Artifact Toolkit configured with bucket `mixed-files-test`
- Bucket contains 5 valid files (.txt, .pdf, .docx, .md, .json) + 4 problematic files: `fake.pdf` (binary .exe renamed), `corrupted.docx` (header stripped), `protected.pdf` (open-password), `pivot-table.xlsx` (complex pivot structures)

## Test Data

| Variant | File Name | Description |
|---|---|---|
| Unsupported format | `fake.pdf` | Binary `.exe` renamed as `.pdf` |
| Corrupted file | `corrupted.docx` | `.docx` with file header stripped/truncated |
| Password-protected | `protected.pdf` | PDF with open-password set |
| Complex pivot table | `pivot-table.xlsx` | Excel with nested/complex unsupported pivot structures |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifact Toolkit configuration page. Click the Indexes tab. | Indexes Tab is displayed. |
| 2 | Click + Create Index. Enter collection suffix `skip_t`. | New index form is ready. |
| 3 | Click Index to start the indexing process. | Status changes to 🔄 In Progress. Real-time progress messages begin appearing. |
| 4 | Observe the progress log while indexing is running. Check whether the job stops when it encounters a problematic file. | The job does NOT stop with ❌ Failed when a problematic file is encountered. |
| 5 | Wait for the run to complete. Check the final status indicator. | Final status = ✅ Completed. |
| 6 | Repeat steps 2–5 for each remaining problematic file variant, using a fresh index suffix each time. | ✅ Completed is reached in all four variants without stopping at ❌ Failed. |

## Expected Final State

✅ Completed is reached in all four variants without stopping at ❌ Failed.

## Pass/Fail Criteria

**Pass:**
- Indexing reaches ✅ Completed in all four file variants
- Job does not stop at ❌ Failed due to any problematic file

**Fail:**
- Indexing stops with ❌ Failed when any problematic file is encountered
- Indexing gets stuck in 🔄 In Progress indefinitely
- An unhandled exception or application crash is shown
