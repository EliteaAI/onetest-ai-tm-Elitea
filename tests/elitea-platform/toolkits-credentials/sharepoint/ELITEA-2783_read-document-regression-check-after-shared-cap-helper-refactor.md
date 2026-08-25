---
id: ELITEA-2783
title: "read_document Regression Check via Artifacts Upload After Shared Cap-Helper Refactor"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, read_document, artifacts, shared-cap-helper]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2783: read_document Regression Check via Artifacts Upload After Shared Cap-Helper Refactor

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that `read_document`'s output-capping behavior is unaffected — i.e. still correct — after PR #517 refactored `read_file_from_sharing_link` to reuse the shared `bound_read_result` cap helper that `read_document` already relied on. This is a regression check scoped specifically to the shared-helper refactor risk.

**Invocation mechanism (important):** `read_document` cannot be exercised via a raw path typed directly in chat — that invocation path does not currently work in the product (manually verified). It must instead be tested by uploading the file to **Artifacts** first, then asking the chat agent to read the uploaded artifact; this internally triggers `read_document`.

**Scope note:** This test does not duplicate `ELITEA-1641` (non-existent-file path) or `ELITEA-1643` (happy-path), which cover `read_document`'s baseline behavior unrelated to this refactor. It also does not duplicate `ELITEA-1785`, which currently describes an invocation mechanism (raw path typed directly in chat) that is unverified and likely stale for the current product behavior; `ELITEA-1785` should be flagged for a separate correction rather than modified here.

## Preconditions

- User is logged in to ELITEA with access to Artifacts and Chat
- An oversized text file (sized to exceed the output cap, consistent with ELITEA-2778) is available for upload
- An oversized `.xlsx` file (sized to exceed the Excel pre-parse guard, consistent with ELITEA-2781) is available for upload

## Test Data

| File | Type | Notes |
|------|------|-------|
| Oversized text file | `.txt` (or similar) | Same class of oversized file used in ELITEA-2778 |
| Oversized Excel workbook | `.xlsx` | Same class of oversized file used in ELITEA-2781 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Upload the oversized text file to Artifacts, then in chat ask the agent to read that uploaded artifact | `read_document` is triggered internally; the response exhibits the same "content too large" guidance behavior as `read_file_from_sharing_link` (structured, self-describing, no provider/LLM crash); `read_document`'s own applicable parameters (e.g. row ranges where applicable) are offered correctly in the guidance |
| 2 | Upload the oversized `.xlsx` file to Artifacts, then in chat ask the agent to read that uploaded artifact | Same Excel over-limit guidance behavior as the sharing-link tool is returned (no crash, guidance matches `read_document`'s actual parameter surface, e.g. `sheet_name` where applicable) |

## Expected Final State

`read_document`, invoked via the Artifacts-upload chat path, continues to correctly cap oversized text and Excel content post-refactor, returning guidance consistent with `read_file_from_sharing_link`'s new behavior, with no regression introduced by sharing the `bound_read_result` helper.

## Pass/Fail Criteria

**Pass:**
- `read_document`'s capping behavior (both text and Excel) matches expectations post-refactor when invoked via the Artifacts-upload path
- Guidance correctly reflects `read_document`'s own parameter surface

**Fail:**
- Cap is missing (oversized content returned in full or causes a provider/LLM crash)
- Guidance is malformed or references parameters `read_document` does not accept
- Any crash or unhandled exception during either upload-and-read flow
