---
id: ELITEA-2782
title: "read_file_from_sharing_link Invalid start_line/end_line Requests Return Explicit Errors"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, start-line, end-line, error-handling, invalid-range]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2782: read_file_from_sharing_link Invalid start_line/end_line Requests Return Explicit Errors

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file_from_sharing_link` returns explicit, informative errors — rather than an empty success — when called with an inverted line range (`start_line` > `end_line`) or with a `start_line` that is far beyond the file's actual line count.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A sharing link to any text file with a known, finite line count is available

## Test Data

| Scenario | Example Values |
|----------|-----------------|
| Inverted range | `start_line = 100`, `end_line = 10` |
| Out-of-range start | `start_line` set far past the file's actual total line count (e.g. `start_line = 1000000` on a file with a few hundred lines) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the text file with `start_line` greater than `end_line` | Explicit error naming the invalid range (e.g. "end_line is before start_line") is returned — not an empty string as if the call succeeded |
| 2 | Call `read_file_from_sharing_link` on the text file with `start_line` set far past the file's actual line count | Explicit error is returned reporting the true total line count and the valid range (e.g. "1..N") — not an empty string as if the call succeeded |

## Expected Final State

Both invalid line-range requests are rejected with explicit, actionable error messages that identify the nature of the problem (inverted range, or out-of-range start) rather than returning an empty or ambiguous "success".

## Pass/Fail Criteria

**Pass:**
- Inverted range (`start_line` > `end_line`) produces an explicit error naming the invalid range
- Out-of-range `start_line` produces an explicit error reporting the true total line count and the valid range

**Fail:**
- Either case silently returns an empty string as if the call succeeded
