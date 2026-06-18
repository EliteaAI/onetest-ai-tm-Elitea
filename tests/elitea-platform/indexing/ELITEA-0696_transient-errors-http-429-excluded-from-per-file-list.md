---
id: ELITEA-0696
title: "Transient Errors (HTTP 429) Excluded From Per-File ❌ List"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0696: Transient Errors (HTTP 429) Excluded From Per-File ❌ List

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that rate-limit or transient infrastructure errors (e.g., HTTP 429) are not surfaced as named file entries in the ❌ section, and do not pollute the per-file summary breakdown.

**Coverage:**
- ❌ section contains only named file entries for files that genuinely failed parsing
- HTTP 429 or other transient errors handled at the system/notification level — not listed as a named file
- Successfully indexed files still counted in ✅ section after transient errors

## Preconditions

- Logged in to {{base_url}} a toolkit connected to a rate-limited data source (e.g., GitHub or SharePoint) configured to produce 429-type responses during large indexing runs
- At least 1 valid file present to confirm ✅ section is populated

## Test Data

- Toolkit: GitHub or SharePoint; source: a large repository or library that triggers rate limiting
- At least 1 valid file present to confirm ✅ section is populated

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger indexing on a source known to produce transient 429 errors during the run. | Indexing starts. |
| 2 | Wait for the run to reach a terminal state; click History tab → select the latest entry. | Summary panel opens. |
| 3 | Inspect the ❌ section entries. | Each ❌ entry is a named file — not a generic HTTP error or '429' string. |
| 4 | Verify no entry in the ❌ section reads 'HTTP 429', 'rate limit', or references a transport error without a file name. | No transient error entry present. |
| 5 | Verify files that succeeded are counted in ✅. | ✅ count > 0. |

## Expected Final State

✅ count > 0.

## Pass/Fail Criteria

**Pass:**
- No HTTP 429 or transient error entry in the ❌ file list
- ❌ section contains only named file entries for genuine parsing failures

**Fail:**
- A "429" or transport-level error appears as a named entry in the ❌ section
- Valid files absent from ✅ due to transient error misclassification
