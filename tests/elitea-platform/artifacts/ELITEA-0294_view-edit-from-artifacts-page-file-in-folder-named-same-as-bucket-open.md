---
id: ELITEA-0294
title: "View/Edit from Artifacts Page: File in Folder Named Same as Bucket Opens Preview Without 400 Error [Parametrized]"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3874]
---
# ELITEA-0294: View/Edit from Artifacts Page: File in Folder Named Same as Bucket Opens Preview Without 400 Error [Parametrized]

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that opening a file stored in a path that contains the bucket name as a folder segment opens the Canvas preview modal successfully — without returning "Failed to fetch file: 400". Both entry points on the Artifacts page are tested (click file name + View/Edit eye icon), across 3 path patterns each using a different file type.

**Coverage (3 path patterns from bug EliteaAI/elitea_issues#3874, one file type per pattern):**
- Pattern 1: `bucket → folder(=bucket_name) → file` — `.txt` — exact scenario from the bug report
- Pattern 2: `bucket → folder(=bucket_name) → any_folder → file` — `.png` — binary image
- Pattern 3: `bucket → any_folder → folder(=bucket_name) → file` — `.md` — markdown text

**Open methods tested per row:**
- Click directly on the file name in the file tree
- Click the View/Edit (eye) icon on the file row

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- An Artifact Toolkit is configured with a bucket named `preview-bucket`
- Artifact Toolkit Test Settings panel is accessible via Toolkits menu
- A small valid `.png` image file is available locally for upload

## Test Data

| # | Path pattern | File type | CreateFile Filename input | Expected full object path |
|---|---|---|---|---|
| 1 | bucket_name/bucket_name/file | `.txt` | `preview-bucket/p1-file.txt` | `preview-bucket/preview-bucket/p1-file.txt` |
| 2 | bucket_name/bucket_name/any_folder/file | `.png` | `preview-bucket/nested-folder/p2-image.png` | `preview-bucket/preview-bucket/nested-folder/p2-image.png` |
| 3 | any_folder/bucket_name/file | `.md` | `other-folder/preview-bucket/p3-file.md` | `preview-bucket/other-folder/preview-bucket/p3-file.md` |

Text/Markdown content: `View/Edit parametrized test content.`
Image file (.png): any small valid .png test image

Open methods per row: click file name + click View/Edit (eye) icon

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → open the Artifact Toolkit → open Test Settings. Select CreateFile. | CreateFile form is shown with Filename, Filedata, Bucket Name, and Filepath fields. |
| 2 | Create all 3 test files by running CreateFile once per row: - Row 1: Filename = `preview-bucket/p1-file.txt`, Filedata = `View/Edit parametrized test content.` - Row 2: Filename = `preview-bucket/nested-folder/p2-image.png`, upload a small test .png image - Row 3: Filename = `other-folder/preview-bucket/p3-file.md`, Filedata = `# Markdown test\nView/Edit parametrized test content.` Click RUN TOOL after each. | All 3 tool runs return success. Files are created at their respective full paths inside bucket `preview-bucket`. |
| 3 | Navigate to Artifacts from the sidebar. Select the `preview-bucket` bucket. | Bucket file tree loads. Folders `preview-bucket/`, `preview-bucket/nested-folder/`, and `other-folder/preview-bucket/` are visible. |
| 4 | **Row 1 — Pattern: bucket_name/bucket_name/file \| .txt \| click file name** Expand folder `preview-bucket/`. Click directly on `p1-file.txt`. | Canvas modal opens. Content `View/Edit parametrized test content.` is displayed. No "Failed to fetch file: 400" error. |
| 5 | Close modal. **Row 1 — same \| View/Edit icon** Click the View/Edit (eye) icon on the `p1-file.txt` row. | Canvas modal opens with the same content. No error. |
| 6 | Close modal. **Row 2 — Pattern: bucket_name/bucket_name/any_folder/file \| .png \| click file name** Expand `preview-bucket/` → expand `nested-folder/`. Click directly on `p2-image.png`. | Preview modal opens. Image is rendered without error. No "Failed to fetch file: 400". |
| 7 | Close modal. **Row 2 — same \| View/Edit icon** Click the View/Edit (eye) icon on the `p2-image.png` row. | Preview modal opens. Image renders correctly. No error. |
| 8 | Close modal. **Row 3 — Pattern: any_folder/bucket_name/file \| .md \| click file name** Expand `other-folder/` → expand `preview-bucket/`. Click directly on `p3-file.md`. | Canvas modal opens. Markdown content is displayed. No "Failed to fetch file: 400" error. |
| 9 | Close modal. **Row 3 — same \| View/Edit icon** Click the View/Edit (eye) icon on the `p3-file.md` row. | Canvas modal opens with the same content. No error. |

## Expected Final State

Canvas modal opens with the same content. No error.

## Pass/Fail Criteria

**Pass:**
- Canvas/preview modal opens without error for ALL 3 rows using BOTH open methods
- `.txt` and `.md` files: content is rendered correctly in the editor
- `.png` file: preview modal opens and image is rendered (no blank modal, no error state)
- No "Failed to fetch file: 400" error for any row or open method

**Fail:**
- "Failed to fetch file: 400" returned for any row via either open method
- Canvas modal blank or shows an error state for any combination
- Image fails to render or shows broken/empty preview for the `.png` row
