---
id: ELITEA-2855
title: "Regression - read_file_from_sharing_link Oversized-Content Cap, Bounded Read, Per-Type Size Validation, Excel Guidance, and read_document Parity"
priority: critical
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, oversized-file, content-too-large, start-line, end-line, bounded-read, test-settings-ui, error-handling, file-size-validation, image-limit, excel, read_document, artifacts, read_file_from_sharing_link]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2855: Regression - read_file_from_sharing_link Oversized-Content Cap, Bounded Read, Per-Type Size Validation, Excel Guidance, and read_document Parity

**Module:** Sharepoint · **Priority:** Critical · **Type:** Regression

**Objective:** Verify, in a single chat session with a SharePoint toolkit configured with delegated permissions attached, that `read_file_from_sharing_link` no longer crashes on oversized content and instead: returns a structured "too large" response; supports `start_line`/`end_line` to narrow into or out of that cap (via chat prompt and via the toolkit's Test Settings UI panel); returns explicit errors for invalid ranges; applies the correct pre-download size cap per file type (document vs. image); returns well-formed guidance for oversized Excel workbooks; and that `read_document` (invoked via Artifacts upload) shows the same capping behavior after sharing the underlying cap helper.

**Coverage:**
- No provider/LLM-level error (`BadRequestError`/"string too long") on oversized reads (issue #6051 original failure)
- Structured "too large" response with totals reflecting the full file, not a requested slice
- `start_line`/`end_line` bounded-read contract, via chat and via the Test Settings UI panel
- Explicit errors for inverted or out-of-range line requests
- Per-file-type pre-download size validation (20MB documents, 3MB images)
- Oversized Excel workbook guidance
- `read_document` parity via Artifacts upload

Scoped only to the pre-parse size/row estimate guard for Excel. Does **not** include a `sheet_name`-parameter step — already covered by the Artifacts-toolkit test `ELITEA-0335` and intentionally not duplicated here.

**Invocation mechanism (important):** `read_document` cannot be exercised via a raw path typed directly in chat — verified not to work in the product. It must be tested by uploading the file to **Artifacts** first, then asking the chat agent to read the uploaded artifact, which internally triggers `read_document` (steps 11–12).

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A chat conversation is open in ELITEA with a SharePoint toolkit configured with delegated permissions attached — currently the **"Epam Sharepoint Delegated"** toolkit is used for this (per issue #6051 steps to reproduce). This exposes `read_file_from_sharing_link` for automatic invocation from a natural-language prompt, and exposes the tool's entry in the toolkit's Test Settings panel in the UI
- User has access to Artifacts in the same chat
- All test files below exist and are shared via sharing links (or available locally for Artifacts upload)

## Test Data

| File | Type | Size | Used For |
|------|------|------|----------|
| Oversized text file | `.md`/`.txt` | ~11MB / ~12,043,364 parsed characters (reproduces original issue #6051 file) | Cap, bounded read, invalid range, Artifacts parity |
| Large non-image document | `.docx`/`.pdf` | > 20MB | Per-type size validation (document cap) |
| Large image | `.png`/`.jpg` | > 3MB | Per-type size validation (image cap) |
| Large multi-sheet Excel workbook | `.xlsx` | Sized to trigger the pre-parse row/size estimate guard | Excel guidance, Artifacts parity |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat and attach a SharePoint toolkit configured with delegated permissions (currently "Epam Sharepoint Delegated") to the conversation | Toolkit attaches successfully; `read_file_from_sharing_link` is available to the agent |
| 2 | In chat, prompt: "Can you call read_file using link tool to read the below file: `<sharing link to oversized text file>`" (no line range mentioned) | Agent automatically invokes `read_file_from_sharing_link` with no `start_line`/`end_line`; call completes with no provider/LLM error; response is a structured "too large" object whose size/length indicator exceeds the reported cap and references `start_line`/`end_line` as the mechanism to narrow the request |
| 3 | In the same chat, prompt the agent to re-read that file but only the first ~50 lines | Agent maps this to `start_line`/`end_line`; plain sliced text for exactly that range is returned — not the "too large" object |
| 4 | Prompt the agent to read a wider range of the same file that still exceeds the cap | "Too large" response is returned again; total-length/line-count info reflects the full file's totals, not just the requested slice |
| 5 | Open this tool's entry in the SharePoint toolkit's Test Settings panel in the UI, and run test calls directly with `start_line`/`end_line` set to the same in-range and out-of-range values as steps 3–4 | `start_line`/`end_line` are present as optional fields in the panel; results are consistent with steps 3–4 |
| 6 | Prompt the agent to read the file with an inverted range (`start_line` > `end_line`, e.g. 100–10) | Explicit error naming the invalid range is returned — not an empty string as if it succeeded |
| 7 | Prompt the agent to read the file with a `start_line` far past its actual line count | Explicit error is returned reporting the true total line count and the valid range |
| 8 | In the same chat, prompt the agent to read the sharing link of the oversized non-image document (> 20MB) | Rejected immediately; error message references the file name and the ~20MB limit; no content is parsed |
| 9 | Prompt the agent to read the sharing link of the oversized image (> 3MB) | Rejected; error message specifically references the 3MB image limit (not the 20MB document limit) |
| 10 | Prompt the agent to read the sharing link of the large multi-sheet `.xlsx` workbook | "Content too large" guidance is returned; no crash or unhandled exception |
| 11 | Upload the oversized text file to **Artifacts**, then in the same chat ask the agent to read the uploaded artifact | `read_document` is triggered internally; response exhibits the same "content too large" guidance behavior as step 2, with no provider/LLM crash |
| 12 | Upload the oversized `.xlsx` workbook to Artifacts, then ask the agent to read that uploaded artifact | Same Excel over-limit guidance as step 10 is returned; no crash; guidance matches `read_document`'s actual parameter surface |

## Expected Final State

Within a single chat session with the toolkit attached once, all of the following hold with no provider/LLM crash at any point: oversized-content capping, bounded-read recovery via chat prompt and via the Test Settings UI panel, explicit invalid-range errors, correct per-file-type pre-download size validation, well-formed Excel guidance, and `read_document` parity via Artifacts upload.

## Pass/Fail Criteria

**Pass:**
- No provider/LLM exception at any point across all 12 steps
- Structured "too large" response with a size/length indicator exceeding the reported cap (steps 2, 4)
- In-range slice returns exactly the requested plain text (step 3); results from the Test Settings panel are consistent with chat behavior (step 5)
- Inverted range and out-of-range start each produce an explicit, informative error (steps 6–7)
- Non-image document > 20MB and image > 3MB are each rejected with a message referencing the correct, type-appropriate limit (steps 8–9)
- Oversized Excel workbook returns "content too large" guidance without crashing (step 10)
- `read_document` via Artifacts upload shows the same capping behavior for both the text file and the Excel workbook (steps 11–12)

**Fail:**
- A provider/LLM exception is raised at any step
- Silent truncated/garbled dump with no "too large" indication
- Total-length/line-count in the "too large" response reflects only the requested range instead of the full file
- `start_line`/`end_line` missing from or non-functional in the Test Settings panel
- Either invalid-range case silently returns an empty string as if it succeeded
- Either file-type rejection message references the wrong limit, or either oversized file is accepted
- Excel workbook crashes instead of returning guidance
- `read_document` via Artifacts upload lacks the cap, crashes, or returns guidance referencing parameters `read_document` doesn't accept
