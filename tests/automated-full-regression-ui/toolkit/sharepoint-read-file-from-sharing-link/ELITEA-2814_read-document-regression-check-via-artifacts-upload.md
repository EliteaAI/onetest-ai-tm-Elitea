---
id: ELITEA-2814
title: "Regression - read_document Output Capping via Artifacts Upload After Shared Cap-Helper Refactor"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, read_document, artifacts, shared-cap-helper]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2814: Regression - read_document Output Capping via Artifacts Upload After Shared Cap-Helper Refactor

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that `read_document`'s output-capping behavior is unaffected after `read_file_from_sharing_link` was refactored to reuse the shared `bound_read_result` cap helper that `read_document` already relied on.

**Invocation mechanism (important):** `read_document` cannot be exercised via a raw path typed directly in chat — verified not to work in the product. It must be tested by uploading the file to **Artifacts** first, then asking the chat agent to read the uploaded artifact, which internally triggers `read_document`.

Does not duplicate `ELITEA-1641` (non-existent-file path) or `ELITEA-1643` (happy-path), which cover baseline behavior unrelated to this refactor.

## Preconditions

- User is logged in to ELITEA with access to Artifacts and Chat
- An oversized text file (same class as used in ELITEA-2811) is available for upload
- An oversized `.xlsx` file (same class as used in ELITEA-2813) is available for upload

## Test Data

| File | Type | Notes |
|------|------|-------|
| Oversized text file | `.txt` (or similar) | Same class of oversized file used in ELITEA-2811 |
| Oversized Excel workbook | `.xlsx` | Same class of oversized file used in ELITEA-2813 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Upload the oversized text file to Artifacts, then in chat ask the agent to read that uploaded artifact | `read_document` is triggered internally; response exhibits the same "content too large" guidance behavior as `read_file_from_sharing_link` (structured, self-describing, no provider/LLM crash) |
| 2 | Upload the oversized `.xlsx` file to Artifacts, then in chat ask the agent to read that uploaded artifact | Same Excel over-limit guidance behavior as the sharing-link tool is returned (no crash, guidance matches `read_document`'s actual parameter surface) |

## Expected Final State

`read_document`, invoked via the Artifacts-upload chat path, continues to correctly cap oversized text and Excel content post-refactor, with no regression introduced by sharing the `bound_read_result` helper.

## Pass/Fail Criteria

**Pass:**
- `read_document`'s capping behavior (text and Excel) matches expectations post-refactor via the Artifacts-upload path

**Fail:**
- Cap is missing or crashes on either upload-and-read flow
- Guidance is malformed or references parameters `read_document` does not accept
