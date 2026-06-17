---
id: ELITEA-0702
title: "File List Per Category Capped at 5 Entries With Truncation Indicator"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0702: File List Per Category Capped at 5 Entries With Truncation Indicator

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that each category section shows at most 5 → filename entries, and when the count exceeds 5 a truncation indicator shows the remaining count.

**Coverage:**
- Exactly 5 file entries shown in a section that has more than 5 files
- Truncation indicator present showing the count of hidden entries
- Section header count reflects the true total (not capped at 5)

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- Bucket contains 8 files that all produce runtime errors

## Test Data

- Bucket: truncation-test; index name: trunc01
- Files: 8 corrupted or renamed-extension files (e.g., broken1.docx through broken8.docx)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index trunc01 → click Index. | Indexing starts. |
| 2 | Wait for terminal state; click History tab → select the latest entry. | Summary panel opens. |
| 3 | Locate the ❌ N documents — Runtime skipped (errors) section. | ❌ section is present. |
| 4 | Count the → filename entries in the ❌ section. | Exactly 5 entries listed. |
| 5 | Verify a truncation indicator is present (e.g., '...and 3 more' or equivalent). | Truncation indicator visible. |
| 6 | Verify the ❌ section header reads ❌ 8 documents. | Header count = 8, not 5. |

## Expected Final State

Header count = 8, not 5.

## Pass/Fail Criteria

**Pass:**
- Exactly 5 file entries visible in the ❌ section
- Truncation indicator present showing at least "3 more" files
- Section header count = 8

**Fail:**
- More than 5 entries displayed without any truncation indicator
- Section header count = 5 instead of 8
- No truncation indicator present when count exceeds 5
