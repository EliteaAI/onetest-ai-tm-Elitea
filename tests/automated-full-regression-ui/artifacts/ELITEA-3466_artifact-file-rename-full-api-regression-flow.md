---
id: ELITEA-3466
title: "Rename Artifact File — Full API Regression Flow (E2E)"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback, automated:API:regression]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3466: Rename Artifact File — Full API Regression Flow (E2E)

**Module:** artifacts · **Priority:** high · **Type:** regression

**Objective:** Exercise all direct-API validation, success, and conflict paths for the artifact file rename endpoint in a single consolidated end-to-end regression pass.

---

## Preconditions

- Valid API credentials/token with `artifacts.edit` permission on the target project/bucket.
- Endpoint under test: `PUT {{base_url}}/api/v2/artifacts/artifact/{bucket_type}/{project_id}/{bucket_name}/?old_name={old_file_name}&new_name={new_file_name}`
- A bucket pre-populated with at least two files, one of which will be used purely as a pre-existing "conflict target".

## Test Data

| Scenario | old_name | new_name | Expected HTTP | Expected Message |
|---|---|---|---|---|
| Happy path | `Test-Plans.docx` | `Test-Plans-Renamed.docx` | 200 | success |
| old == new | `Test-Plans-Renamed.docx` | `Test-Plans-Renamed.docx` | 400 | "old_name and new_name must be different" |
| Source missing | `DoesNotExist.docx` | `New.docx` | 404 | "Source file not found: DoesNotExist.docx" |
| Missing query params | (omit `new_name`) | — | 400 | "old_name and new_name query parameters are required" |
| Destination already exists | `Test-Plans-Renamed.docx` | `<name of existing second file>` | 4xx | "Destination file already exists: <name>" |
| Repeat same request after first rename succeeded | `Test-Plans.docx` (already renamed) | `Another.docx` | 404 | "Source file not found" |
| New name contains a slash | `Test-Plans-Renamed.docx` | `Test/Plans.docx` | — (expected: rejected) | Not confirmed by the checklist — expected to mirror the UI-side block on this character; no specific code/message is asserted |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the happy-path rename request. | 200 OK; file is renamed; visible under new name via a follow-up list/get call. |
| 2 | Send a request with `old_name == new_name` (using the now-current name). | 400 "old_name and new_name must be different". |
| 3 | Send a request with a non-existent `old_name`. | 404 "Source file not found: <name>". |
| 4 | Send a request omitting the `new_name` query parameter. | 400 "old_name and new_name query parameters are required". |
| 5 | Send a request whose `new_name` matches an already-existing file in the same bucket. | Blocked with "Destination file already exists: <name>". |
| 6 | Immediately repeat step 1's exact request (same old_name, now already renamed). | 404 "Source file not found" (no race-condition crash or 500). |
| 7 | Send a rename request where `new_name` contains a slash (e.g. `Test/Plans.docx`). | Expected to be rejected as invalid input, consistently with the UI-side block on the same character. The exact status code and message are not asserted here, since they were not confirmed as a passing behavior in the checklist. |
| 8 | Inspect the response bodies/headers from steps 2–7 for leaked internal details (stack traces, file system paths, DB identifiers). | All messages are user-appropriate and specific to the validation failure; no internal implementation details are present. |

## Expected Final State

All direct-API validation, success, and conflict paths for the rename endpoint — including required-parameter checks, duplicate-name conflicts, and disallowed-character validation — are exercised in one pass.

## Pass/Fail Criteria

**Pass:**
- Steps 1–6 and 8 behave exactly as specified.
- Step 7's slash-containing request is rejected as invalid input.

**Fail:**
- Any step deviates from its specified status code or message.
- The slash-containing request in step 7 is accepted instead of rejected.
- Any response leaks internal implementation details.
