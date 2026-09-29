---
id: ELITEA-3471
title: "Artifact File Rename — Direct API Validation (Old==New, Missing Source, Missing Parameter, Duplicate Target, Repeat Rename, Slash-Containing Name)"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3471: Artifact File Rename — Direct API Validation (Old==New, Missing Source, Missing Parameter, Duplicate Target, Repeat Rename, Slash-Containing Name)

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that the artifact file rename API endpoint returns precise, non-leaking validation errors for malformed, duplicate, and repeat requests, and rejects a slash-containing new name.

---

## Preconditions

- Valid API credentials with `artifacts.edit` permission on a test bucket containing at least one file.
- Bucket additionally contains `Existing.docx` (already-existing duplicate-target file) and `Source.docx` (to be renamed, for the repeat-rename scenario).

## Test Data

| Scenario | old_name | new_name | Expected HTTP | Expected Message |
|---|---|---|---|---|
| old == new | `File.docx` | `File.docx` | 400 | "old_name and new_name must be different" |
| Source missing | `Missing.docx` | `New.docx` | 404 | "Source file not found: Missing.docx" |
| new_name omitted | `File.docx` | (omitted) | 400 | "old_name and new_name query parameters are required" |
| Destination already exists | `File.docx` | `Existing.docx` (already exists) | 4xx | "Destination file already exists: Existing.docx" |
| Repeat request after first rename succeeded | `Source.docx` (already renamed to `Renamed.docx`) | any `new_name` | 404 | "Source file not found" |
| new_name contains a slash | `File.docx` | `Sub/File.docx` | — (expected: rejected) | Not confirmed by the checklist — expected to mirror the UI-side block on this character; no specific code/message is asserted |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send `PUT .../artifact/.../?old_name=File.docx&new_name=File.docx`. | 400 "old_name and new_name must be different". |
| 2 | Send `PUT .../artifact/.../?old_name=Missing.docx&new_name=New.docx` where `Missing.docx` does not exist in the bucket. | 404 "Source file not found: Missing.docx". |
| 3 | Send `PUT .../artifact/.../?old_name=File.docx` with `new_name` omitted entirely. | 400 "old_name and new_name query parameters are required". |
| 4 | Send `PUT .../artifact/.../?old_name=File.docx&new_name=Existing.docx`, where `Existing.docx` already exists in the bucket. | Rename attempt returns an error — "Destination file already exists: Existing.docx"; neither file is overwritten or modified. |
| 5 | Send `PUT .../artifact/.../?old_name=Source.docx&new_name=Renamed.docx`. | 200 OK; file is renamed. |
| 6 | Immediately resend the identical request (`old_name=Source.docx&new_name=Renamed.docx`). | 404 "Source file not found" — `Source.docx` no longer exists to be renamed; `Renamed.docx` is unaffected by the failed repeat request. |
| 7 | Send `PUT .../artifact/.../?old_name=File.docx&new_name=Sub/File.docx`. | Expected to be rejected as invalid input, consistently with the UI-side block on the same character. The exact status code and message are not asserted here, since they were not confirmed as a passing behavior in the checklist. |
| 8 | Confirm no unintended file state changed as a result of any of the requests above. | Bucket contents identical before and after, aside from the intentional `Source.docx` → `Renamed.docx` rename in step 5. |
| 9 | Inspect all responses for leaked internal details (stack traces, file system paths, DB identifiers). | No internal implementation details are present in any response; all messages are specific and user-appropriate. |

## Expected Final State

The rename endpoint returns precise, correctly-coded, non-leaking validation errors for malformed requests; duplicate-destination and repeat-after-success requests are both rejected cleanly (this is correct, expected behavior, not a defect); and the endpoint is expected to reject filenames containing disallowed characters — all with zero unintended side effects.

## Pass/Fail Criteria

**Pass:** The old==new, missing-source, missing-parameter, duplicate-target, and repeat-rename responses each match their expected HTTP code and message exactly; the slash-containing request is rejected as invalid input; no unintended file state changes; no internal details leaked.
**Fail:** Any of the above responses uses the wrong status code or a vague/incorrect message; the slash-containing request is accepted instead of rejected; a conflicting or repeat rename succeeds unexpectedly; an unintended file change occurs; or internal implementation details are leaked.
