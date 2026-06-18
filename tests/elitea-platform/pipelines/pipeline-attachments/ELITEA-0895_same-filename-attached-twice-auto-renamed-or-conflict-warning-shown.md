---
id: ELITEA-0895
title: "Same Filename Attached Twice — Auto-Renamed or Conflict Warning Shown"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0895: Same Filename Attached Twice — Auto-Renamed or Conflict Warning Shown

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching the same filename twice in the pipeline chat results in auto-renaming or a clear conflict warning — not a silent overwrite.

**Coverage:**
- Second file with same name auto-renamed with timestamp or suffix
- OR conflict warning shown to the user
- Original file not silently overwritten

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

- File 1: image.png
- File 2: image.png (duplicate name)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Attach image.png (first upload). Type a prompt and click Send. | First upload succeeds; image.png stored in attachments bucket. |
| 2 | In the same chat session, attach another file named image.png (second upload). | Second file is either: (a) auto-renamed (e.g., image_20260520_143022.png) or (b) a conflict warning is displayed. |
| 3 | Observe the attachment thumbnail label. | Second file has a distinct name (not identical to first) OR user is prompted about the conflict. |
| 4 | Navigate to Artifacts → attachments bucket. | Both files are distinguishable — no silent overwrite occurred. |

## Expected Final State

Both files are distinguishable — no silent overwrite occurred.

## Pass/Fail Criteria

**Pass:**
- Second file auto-renamed or conflict warning shown
- Both files distinguishable in attachments bucket

**Fail:**
- Second file silently overwrites the first
- No indication of naming conflict given to the user
