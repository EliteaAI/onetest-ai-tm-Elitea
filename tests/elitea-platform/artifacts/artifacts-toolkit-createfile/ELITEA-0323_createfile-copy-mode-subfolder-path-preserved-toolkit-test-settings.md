---
id: ELITEA-0323
title: "createFile (copy mode): Subfolder Path Preserved (Toolkit Test Settings)"
priority: critical
type: functional
module: artifacts-toolkit-createfile
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3690]
---
# ELITEA-0323: createFile (copy mode): Subfolder Path Preserved (Toolkit Test Settings)

**Module:** Artifacts Toolkit Createfile · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `createFile` in copy mode (`filepath` set, `filedata` empty) creates the copy at the subfolder path specified in `filename`, not at the bucket root. Also covers recreation: re-running copy to the same subfolder path overwrites correctly.

**Coverage:**
- `createFile` copy mode with `filename=copies/source_copy.txt` and `filepath=/{bucket}/source.txt`
- File copied to correct subfolder path, not to root
- Response `filepath` and `filename` reflect the full subfolder path
- Running the copy again to the same subfolder path recreates/overwrites correctly at the subfolder

## Preconditions

- Logged in to next.elitea.ai, Private project
- Artifact Toolkit with CreateFile enabled
- Toolkit canvas page accessible via Toolkits menu
- Artifacts bucket page open in a separate browser tab for visual verification

## Test Data

- Filename: copies/source_copy.txt
- Filedata: (empty)
- Filepath: /[bucket]/source.txt
- Re-run: same parameters to test recreation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifacts bucket in a separate browser tab (Artifacts menu → select the bucket). | Bucket file tree is visible and ready for checking. |
| 2 | Check the bucket tab for source.txt at root. If it does not exist, go to Test Settings → CreateFile, set Filename = source.txt and Filedata = source content, click RUN TOOL, then refresh the bucket tab to confirm. | source.txt is visible at the bucket root. |
| 3 | In Test Settings, select CreateFile. Set Filename = copies/source_copy.txt, Filepath = /[bucket]/source.txt, leave Filedata empty. Click RUN TOOL. | Response appears in the chat panel. |
| 4 | Inspect the response JSON: verify filepath = /[bucket]/copies/source_copy.txt and filename = copies/source_copy.txt — not bare source_copy.txt. | Both fields contain the full subfolder path copies/source_copy.txt. |
| 5 | Switch to the Artifacts bucket tab and refresh. | source_copy.txt exists inside the copies/ subdirectory. No source_copy.txt at the bucket root. |
| 6 | Repeat step 3 — run the same copy call again (Filename = copies/source_copy.txt, Filepath = /[bucket]/source.txt). Click RUN TOOL. | Tool succeeds; response JSON again shows full path copies/source_copy.txt. |
| 7 | Switch to the Artifacts bucket tab and refresh. | File at copies/source_copy.txt is intact (overwritten). Bucket root remains clean — no source_copy.txt appeared there. |

## Expected Final State

File at copies/source_copy.txt is intact (overwritten). Bucket root remains clean — no source_copy.txt appeared there.

## Pass/Fail Criteria

**Pass:**
- Response filepath and filename always reflect full subfolder path copies/source_copy.txt
- File exists inside copies/ in Artifacts bucket UI; no file at bucket root
- Re-run: file overwritten at copies/ path; root stays clean

**Fail:**
- Response strips the subfolder prefix (filepath = /bucket/source_copy.txt)
- File appears at bucket root instead of copies/
- Duplicate created at root on re-run
