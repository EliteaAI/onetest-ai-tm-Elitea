---
id: ELITEA-3085
title: "Toolkit History Records Reindex Error"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, history]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3085: Toolkit History Records Reindex Error

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that failed reindex attempts appear in Toolkit History with error details and indication that the previous index was retained.

**Coverage:**
- Toolkit History entry created for failed reindex
- Error details visible in history
- Previous index retention is indicated

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed toolkit index (Confluence, Jira, GitHub, etc.)
- Access to Toolkit History

## Test Data

- Index: Any toolkit index with external integration
- Failure method: Token revocation or network block

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Toolkit page (e.g., Confluence Toolkit). | Toolkit page displayed. |
| 2 | Open the History tab for the toolkit. | Toolkit History displayed. |
| 3 | Note current history entries. | Entries noted. |
| 4 | Cause reindex failure (e.g., revoke token). | Failure condition set. |
| 5 | Navigate to Indexes, select the toolkit's index, initiate Reindex. | Reindex fails. |
| 6 | Return to Toolkit History tab. | History refreshed. |
| 7 | Verify new entry for failed reindex. | Entry shows reindex attempt. |
| 8 | Verify error details are included. | Entry shows error message (e.g., "401 Unauthorized"). |
| 9 | Verify entry indicates index retention. | Entry mentions "previous index retained" or similar. |

## Expected Final State

Toolkit History contains detailed record of failed reindex with error cause and data preservation note.

## Pass/Fail Criteria

**Pass:**
- Toolkit History entry created for failure
- Error details are specific
- Index retention is indicated
- Entry is easily found in history

**Fail:**
- No history entry for failed reindex
- Error details missing or vague
- No indication of data preservation
- History does not reflect failure
