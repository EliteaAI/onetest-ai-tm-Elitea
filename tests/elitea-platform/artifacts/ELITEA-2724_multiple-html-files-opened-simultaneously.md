---
id: ELITEA-2724
title: "Multiple HTML files can be opened simultaneously"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple HTML files exist in Artifacts

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File 1 | test_file_1_under_1mb.htm |
| File 2 | test_file_2_between_1_3mb_structured.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open first HTML file in Canvas | First file displays |
| 2 | Navigate back to Artifacts (without closing Canvas) | Artifacts list shows |
| 3 | Open second HTML file | Second file opens |
| 4 | Observe both Canvas instances | Both files are accessible |
| 5 | Switch between the two files | Can access both |
| 6 | Make changes in one file | Changes appear in that file only |
| 7 | Verify the other file is unaffected | Second file unchanged |

## Expected Final State

- Both files are accessible in separate Canvas instances/tabs
- Switching between files works correctly
- Each file maintains its own state (Preview/Raw mode, edits)
- No interference between files

## Pass/Fail Criteria

**Pass:**
- Second file opens successfully
- Both files are accessible
- Switching between files works
- Each file maintains independent state

**Fail:**
- Cannot open second file
- First file closes when opening second
- Files interfere with each other
- State is shared incorrectly between files
