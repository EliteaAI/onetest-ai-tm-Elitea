---
id: ELITEA-0723
title: "Regression: All-Valid-File Indexing Still Completes With Correct Full Count"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0723: Regression: All-Valid-File Indexing Still Completes With Correct Full Count

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify the skip-and-continue change does not break the standard happy-path — when all bucket files are valid, indexing completes with count equal to total file count and no unintended skips.

**Coverage:**
- All-valid bucket indexing reaches ✅ Completed
- Document count equals total file count — no false skips
- No "Index processing error" or "Unable to extract files" in notifications
- All valid files' content is retrievable via `search_index` post-indexing

## Preconditions

- Logged in to {{base_url}}
- Artifact Toolkit with `all-valid-test` bucket containing ONLY valid supported files

## Test Data

- Bucket: `all-valid-test`
- Files: `doc1.txt`, `doc2.pdf`, `doc3.docx`, `doc4.md`, `doc5.json` (each with unique content)
- Expected indexed count: `5`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact Toolkit → Indexes Tab. Create a new index for `all-valid-test` (suffix: `happy`). Click Index. | Status changes to 🔄 In Progress. |
| 2 | Wait for completion. Check the final status. | Status = ✅ Completed. |
| 3 | Read the document count from the sidebar card and Index Detail header. | Count = 5 in both locations. No unexpected skip count shown. |
| 4 | Open the Notifications panel. Check the completion notification text. | No "Index processing error" or "Unable to extract files" text present. |
| 5 | Open Test Settings → select `search_index` → run a query targeting unique content from each of the 5 files in turn. | All 5 files' content is retrievable. |

## Expected Final State

All 5 files' content is retrievable.

## Pass/Fail Criteria

**Pass:**
- Status = ✅ Completed
- Document count = 5 (no false skips)
- No error messages in notifications
- All 5 files' content searchable

**Fail:**
- Status = ❌ Failed
- Count < 5 (false skips of valid files)
- Error message present in notifications
- Any valid file's content not found via search
