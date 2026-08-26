---
id: ELITEA-2811
title: "Regression - read_file_from_sharing_link Oversized File Cap, Bounded Read Recovery, and Invalid Range Errors"
priority: critical
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, oversized-file, content-too-large, start-line, end-line, bounded-read, test-settings-ui, error-handling, read_file_from_sharing_link]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2811: Regression - read_file_from_sharing_link Oversized File Cap, Bounded Read Recovery, and Invalid Range Errors

**Module:** Sharepoint · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that invoking `read_file_from_sharing_link` on an oversized file no longer raises a provider-level error and instead returns a structured "too large" response; that `start_line`/`end_line` correctly narrow a request into or out of that cap (including from the toolkit's Test Settings UI panel); and that invalid line ranges return explicit errors rather than empty success.

**Coverage:**
- No provider/LLM-level error (`BadRequestError`/"string too long") on oversized reads (issue #6051 original failure)
- Structured "too large" response with totals reflecting the full file, not a requested slice
- `start_line`/`end_line` bounded-read contract, including via the Test Settings UI panel
- Explicit errors for inverted or out-of-range line requests

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A text file sized to reproduce the original failure (~11MB / ~12,043,364 parsed characters) exists and is shared via a sharing link
- The SharePoint toolkit is configured, `read_file_from_sharing_link` is accessible via chat/agent, and its entry is visible in the toolkit's Test Settings panel in the UI

## Test Data

| Field | Value |
|-------|-------|
| Oversized file | ~11MB / ~12,043,364 parsed characters |
| In-range slice | `start_line`/`end_line` covering approximately the first 50 lines |
| Wider (still too large) slice | `start_line`/`end_line` covering a range that still exceeds `max_output_chars` |
| Inverted range | `start_line = 100`, `end_line = 10` |
| Out-of-range start | `start_line` far past the file's actual total line count (e.g. `1000000` on a file with a few hundred lines) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Via chat/agent, invoke `read_file_from_sharing_link` on the oversized file with no `start_line`/`end_line` | Call completes without any provider/LLM error; response is a structured, self-describing "too large" object (not silent truncation, not a raw partial dump) whose size/length indicator is present and exceeds the reported cap; the response references `start_line`/`end_line` as the mechanism to narrow the request |
| 2 | Call the tool again with a small in-range slice (first ~50 lines) | Plain sliced text is returned for exactly that requested range — not the "too large" object |
| 3 | Call the tool again with a wider slice that still exceeds the cap | "Too large" response is returned again; any total-length/line-count information reflects the full file's totals, not just the requested slice |
| 4 | Open this tool's entry in the SharePoint toolkit's Test Settings panel in the UI, locate `start_line`/`end_line`, and run a test call from the panel using the same in-range and out-of-range values as steps 2–3 | `start_line`/`end_line` are present as optional fields in the panel; results from the panel are consistent with steps 2–3 |
| 5 | Call the tool with an inverted range (`start_line` > `end_line`) | Explicit error naming the invalid range is returned — not an empty string as if the call succeeded |
| 6 | Call the tool with a `start_line` far past the file's actual line count | Explicit error is returned reporting the true total line count and the valid range — not an empty string |

## Expected Final State

The tool call completes end-to-end with no provider exception on oversized input; `start_line`/`end_line` correctly slice or cap depending on range, with totals in the "too large" response always reflecting the full file; the same parameters work identically from the Test Settings UI panel; and invalid ranges produce explicit, actionable errors rather than empty success.

## Pass/Fail Criteria

**Pass:**
- No provider/LLM exception at any point
- Structured "too large" response with a size/length indicator exceeding the reported cap
- In-range slice returns exactly the requested plain text; out-of-range slice returns "too large" with full-file totals
- `start_line`/`end_line` present and functional in the Test Settings panel, consistent with chat behavior
- Inverted range and out-of-range start each produce an explicit, informative error

**Fail:**
- A provider/LLM exception is raised
- Silent truncated/garbled dump with no "too large" indication
- Total-length/line-count in the "too large" response reflects only the requested range
- `start_line`/`end_line` missing from or non-functional in the Test Settings panel
- Either invalid-range case silently returns an empty string as if it succeeded
