---
id: ELITEA-0288
title: "Artifact Toolkit — Subfolder Files Are Indexed (Not Folders) and Searchable from Index Page, Toolkit Test Panel, and Chat"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3930, ProjectAlita/projectalita.github.io#3613]
---
# ELITEA-0288: Artifact Toolkit — Subfolder Files Are Indexed (Not Folders) and Searchable from Index Page, Toolkit Test Panel, and Chat

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when an Artifact toolkit indexes a bucket with subfolders, only the files inside those subfolders are indexed (not folder entries), and search returns actual file content — verified from the Index page, Toolkit test panel, and Chat.

**Coverage:**
- Indexed file count reflects actual files inside subfolders, not folder entries
- Indexed items list contains files with `type: file`; folder entries (`type: folder`) are NOT indexed
- `search_index` from the Toolkit test panel returns file content, no folder parse errors
- `search_index` from Chat returns file content from subfolder files correctly
- No `"Error during content parsing for file folder/"` entries appear in any search result

## Preconditions

- Logged in to the ELITEA platform at {{base_url}}
- Browser: Chrome (latest stable)
- An Artifact bucket exists with this structure: bucket → subfolder/ → file1.txt, file2.txt (files contain known searchable text)
- An Artifact toolkit is configured pointing to that bucket
- An agent with the Artifact toolkit attached exists (for Chat verification)

## Test Data

| Item | Value |
|---|---|
| Bucket structure | bucket-test → subfolder/ → file1.txt, file2.txt |
| file1.txt content | "hello from subfolder" |
| file2.txt content | "index test content" |
| search_index query | hello from subfolder |
| Expected indexed count | ≥ 2 (files only, no folders)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Go to Artifacts. Confirm the bucket contains subfolder/ with file1.txt (content: "hello from subfolder") and file2.txt (content: "index test content") inside. | Subfolder and both files are visible in the bucket browser. |
| 2 | Go to Toolkits. Open the Artifact toolkit linked to the bucket. Navigate to the Index tab. Create a new index (or re-index if one exists). Wait for status to reach Completed. | Indexing completes successfully. Status shows Completed. |
| 3 | Check the indexed file count shown on the Index page. | Indexed count is ≥ 2, reflecting the actual files inside the subfolder — not 0, and not just the number of folders. |
| 4 | Open the indexed items list. Review what items are listed and their types. | file1.txt and file2.txt appear with type: file. The subfolder entry (subfolder/) does NOT appear as an indexed item. No folder entries with type: folder are listed. |
| 5 | Go to the Toolkit Test panel. Run search_index with query: "hello from subfolder". | Results include a match with page_content: "hello from subfolder" and name: "file1.txt". No result contains page_content with "Error during content parsing for file folder/". |
| 6 | Go to Chat. Open the agent that has the Artifact toolkit. Send: Search the index for "hello from subfolder". | The chat response returns content from file1.txt. No folder parse error message appears in the response. |

## Expected Final State

The chat response returns content from file1.txt. No folder parse error message appears in the response.

## Pass/Fail Criteria

**Pass:**
- Indexed count ≥ 2, matching actual files inside the subfolder
- Indexed items list shows files with `type: file`; no folder entries (`type: folder`) appear as indexed items
- `search_index` from Toolkit test panel returns file content with correct `name` and `page_content`
- `search_index` from Chat returns file content from subfolder files
- No `"Error during content parsing for file folder/: a bytes-like object is required, not 'dict'"` in any result

**Fail:**
- Indexed count is 0 or matches only folder count
- Only folder entries appear in the indexed items list (files absent)
- Folder entries appear as indexed items in the list
- `search_index` returns folder parse errors instead of file content
- Chat search returns no useful results or returns folder error entries
