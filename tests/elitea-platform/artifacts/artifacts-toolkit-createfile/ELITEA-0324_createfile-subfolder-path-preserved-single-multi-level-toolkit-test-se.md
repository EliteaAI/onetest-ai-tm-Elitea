---
id: ELITEA-0324
title: "createFile: Subfolder Path Preserved — Single & Multi-Level (Toolkit Test Settings)"
priority: critical
type: functional
module: artifacts-toolkit-createfile
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3690]
---
# ELITEA-0324: createFile: Subfolder Path Preserved — Single & Multi-Level (Toolkit Test Settings)

**Module:** Artifacts Toolkit Createfile · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `createFile` in filedata mode correctly preserves both single-level and multi-level subfolder paths in the `filename` parameter — including when a file with the same bare name already exists — and that the created file is accessible and listed with the correct path.

**Coverage:**
- `createFile` with single-level subfolder: `folder/createfile_test.txt`
- `createFile` with multi-level subfolder: `a/b/c/deep.txt`
- File pre-exists at bucket root with the same bare name → createFile with subfolder path correctly places/recreates the file at the subfolder path, not at root
- Response JSON `filepath` and `filename` reflect the full subfolder path (not bare filename)
- File visible in Artifacts bucket UI at the correct subfolder location
- `ListFiles` returns the file with the full subfolder path

## Preconditions

- Logged in to next.elitea.ai, Private project
- Artifact Toolkit with CreateFile and ListFiles enabled
- Toolkit canvas page accessible via Toolkits menu
- Artifacts bucket page open in a separate browser tab for visual verification

## Test Data

| Scenario | Filename | Filedata |
|---|---|---|
| Single-level | folder/createfile_test.txt | single level content |
| Multi-level | a/b/c/deep.txt | multi level nested content |
| Recreation | folder/createfile_test.txt | recreated content |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifacts bucket in a separate browser tab (Artifacts menu → select the bucket). | Bucket file tree is visible and ready for checking. |
| 2 | In the main tab, navigate to Toolkits → select the Artifact Toolkit → open canvas page. | Toolkit canvas with Test Settings panel is displayed. |
| 3 | In Test Settings, select tool CreateFile. | CreateFile form shows fields: Filename, Bucket Name, Filedata, Filepath. |
| 4 | Set Filename = folder/createfile_test.txt, Filedata = single level content. Leave Filepath and Bucket Name empty. Click RUN TOOL. | Response JSON appears in the chat panel. |
| 5 | Inspect the response JSON: verify that filepath = /[bucket]/folder/createfile_test.txt and filename = folder/createfile_test.txt — NOT bare createfile_test.txt. | Both fields contain the full subfolder path, not the bare filename. |
| 6 | Switch to the Artifacts bucket tab and refresh the page. | createfile_test.txt appears inside the folder/ subdirectory. No createfile_test.txt exists at the bucket root. |
| 7 | Back in Test Settings, switch to ListFiles and run it once. | folder/createfile_test.txt appears in the listing with the full subfolder path. No bare createfile_test.txt at root level. |
| 8 | Return to CreateFile. Set Filename = folder/createfile_test.txt, Filedata = recreated content. Click RUN TOOL. | Tool succeeds; response JSON again shows filepath = /[bucket]/folder/createfile_test.txt. |
| 9 | Switch to the Artifacts bucket tab and refresh. | File still appears at folder/createfile_test.txt. No new file at the bucket root. File was overwritten at the correct subfolder path. |
| 10 | Return to CreateFile. Set Filename = a/b/c/deep.txt, Filedata = multi level nested content. Click RUN TOOL. | Response JSON: filepath = /[bucket]/a/b/c/deep.txt, filename = a/b/c/deep.txt. |
| 11 | Switch to the Artifacts bucket tab and refresh. | deep.txt exists inside a/b/c/. No deep.txt at the bucket root, and no deep.txt at a/ or a/b/. |

## Expected Final State

deep.txt exists inside a/b/c/. No deep.txt at the bucket root, and no deep.txt at a/ or a/b/.

## Pass/Fail Criteria

**Pass:**
- Response filepath and filename always include full subfolder path (never bare filename)
- Single-level: createfile_test.txt appears inside folder/ in Artifacts bucket; no root copy
- Recreation: file overwritten at folder/createfile_test.txt; bucket root stays clean
- Multi-level: deep.txt appears inside a/b/c/ only; no copies at any intermediate or root level

**Fail:**
- Response strips subfolder (e.g., filepath = /bucket/createfile_test.txt)
- File appears at bucket root instead of the specified subfolder
- Duplicate file created at root when subfolder path was given
