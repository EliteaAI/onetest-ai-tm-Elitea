---
id: ELITEA-2830
title: "Unsupported Items List File Formats"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, unsupported, formats]
requirements: [EL-6229]
---
# ELITEA-2830: Unsupported Items List File Formats

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that items in the "Not indexed" (unsupported) category list the unsupported file extensions or types.

**Coverage:**
- Not indexed section shows count of unsupported items
- Unsupported file formats are listed
- Format list is readable and clear
- Multiple formats shown when applicable

## Preconditions

- Logged in to {{base_url}} with permissions to create indexes
- A storage bucket containing files with unsupported formats:
  - .ai (Adobe Illustrator)
  - .raw (Raw image)
  - .render (Render file)
  - .tfss (Custom format)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Artifacts toolkit |
| Bucket | Bucket with .ai, .raw, .render, .tfss files |
| Expected Unsupported Count | 4 (or count matching prepared files) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select an Artifacts toolkit. | Toolkit details page opens. |
| 2 | Create a new index on the bucket containing unsupported file types. | Index creation initiated. |
| 3 | Wait for indexing to complete. | Status shows Completed or Partially Indexed. |
| 4 | Open Index History → view the summary. | Summary displays. |
| 5 | Locate the "Not indexed" section. | Not indexed section visible. |
| 6 | Verify the section shows count of unsupported items. | Count matches number of unsupported files. |
| 7 | Verify the unsupported formats are listed. | Shows "Unsupported formats: .ai, .raw, .render, .tfss" or similar. |
| 8 | Verify the format list is readable and not truncated. | All formats visible or "and N more" indicator if many. |

## Expected Final State

Not indexed section displays count of unsupported items with a clear list of the unsupported file formats.

## Pass/Fail Criteria

**Pass:**
- Not indexed section shows correct count
- Unsupported formats listed clearly
- Format extensions displayed (e.g., ".ai, .raw")
- List is readable and complete

**Fail:**
- No formats listed
- Incorrect count
- Technical format codes instead of extensions
- Formats truncated without indicator
