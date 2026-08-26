---
id: ELITEA-2779
title: "read_file_from_sharing_link Bounded Read Contract (start_line/end_line) and Test Settings UI Exposure"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, start-line, end-line, bounded-read, test-settings-ui]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2779: read_file_from_sharing_link Bounded Read Contract (start_line/end_line) and Test Settings UI Exposure

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file_from_sharing_link` correctly supports the new `start_line`/`end_line` parameters to narrow a request into or out of the oversized-content cap, that the "too large" response always reports totals for the full file (not the requested slice), and that `start_line`/`end_line` are exposed and usable as optional fields from the SharePoint toolkit's Test Settings panel in the UI.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- The same oversized text file used in ELITEA-2778 (~11MB / ~12,043,364 parsed characters) is available via a sharing link
- The SharePoint toolkit is configured and its `read_file_from_sharing_link` tool entry is visible in the toolkit's Test Settings panel in the UI

## Test Data

| Field | Value |
|-------|-------|
| Oversized file | Same file as ELITEA-2778 (~11MB / ~12,043,364 parsed characters) |
| In-range slice | `start_line`/`end_line` covering approximately the first 50 lines |
| Wider (still too large) slice | `start_line`/`end_line` covering a range that still exceeds `max_output_chars` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the oversized file with no `start_line`/`end_line` provided | Structured "too large" response is returned, and it references `start_line`/`end_line` as the mechanism to narrow the request |
| 2 | Call the tool again with a small in-range slice (e.g. `start_line`/`end_line` covering the first ~50 lines) | Plain sliced text is returned for exactly that requested range — not the "too large" object |
| 3 | Call the tool again with a wider slice that is still too large to fit within the cap | "Too large" response is returned again; any total-length/line-count information in this response reflects the full file's totals, not just the requested slice |
| 4 | Open this tool's entry in the SharePoint toolkit's Test Settings panel in the UI, locate `start_line`/`end_line`, and run a test call from the panel using the same in-range and out-of-range values as steps 2–3 | `start_line`/`end_line` are present as optional fields in the panel; the test call results from the panel are consistent with the behavior observed in steps 1–3 |

## Expected Final State

`start_line`/`end_line` correctly slice the file when the requested range fits the cap, correctly trigger the "too large" response when it does not, total-length/line-count reporting in the "too large" response always reflects the full file, and the same parameters are present and functional when exercised from the Test Settings UI panel.

## Pass/Fail Criteria

**Pass:**
- In-range slice returns exactly the requested plain text
- Out-of-range/too-large slice returns the "too large" object, with totals reflecting the full file
- `start_line`/`end_line` are present as optional fields in the Test Settings panel and a test call from there is consistent with steps 1–3

**Fail:**
- Slicing is incorrect, or the oversized-vs-fits distinction is wrong
- Total-length/line-count in the "too large" response reflects only the requested range instead of the full file
- `start_line`/`end_line` are missing from, or non-functional in, the Test Settings panel
