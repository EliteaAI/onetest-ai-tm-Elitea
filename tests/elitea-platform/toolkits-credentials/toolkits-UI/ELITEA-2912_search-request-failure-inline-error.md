---
id: ELITEA-2912
title: "Search Page — Search Request Failure (Inline Error)"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, search, error-handling, needs-data-confirmation]
requirements: []
---
# ELITEA-2912: Search Page — Search Request Failure (Inline Error)

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify the Search page shows a clear, distinct inline error when a submitted search request fails, and that Search Settings remain available after the error. This test covers only a search request failure, not an indexing failure (see ELITEA-2908 for indexing errors).

**Coverage:**
- A failed search request produces a clear inline error in the Results panel
- The error is visually distinct from a simple empty-required-field validation message
- Search Settings remain displayed after the error

## ⚠️ Data/Execution Dependency

There is currently no documented, deterministic mechanism for making a search request itself fail (as opposed to an empty/invalid-field validation message). Do not substitute an unverified guess (e.g., an arbitrary out-of-range value) when executing this test — confirm the actual failure trigger with the environment owner/dev/QA first and record it in the Test Data section below.

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing Index with completed indexing data
- **A confirmed, documented input/setup that causes the search request itself to fail — TO BE FILLED IN once confirmed with the environment owner/dev/QA. Do not execute this test until this precondition is met.**

## Test Data

| Field | Value |
|-------|-------|
| Index | Any completed Index |
| Failure input | `{{confirmed_request_failure_input}}` — placeholder; replace with the actual confirmed value once known |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an Index's Search page and click "Select Tool". | Tool list opens. |
| 2 | Select a supported search tool. | Parameters for the tool are displayed. |
| 3 | Enter the confirmed request-failure input/setup (see Test Data) in the required fields. | Values are accepted by the form. |
| 4 | Click "Search". | Results panel displays a loading state while the request runs. |
| 5 | Wait for the request to complete. | A clear inline error is displayed in the Results panel, describing the failure. |
| 6 | Inspect Search Settings. | Values entered in step 3 remain displayed. |

## Expected Final State

A clear inline error is shown for the failed search request; Search Settings remain populated.

## Pass/Fail Criteria

**Pass:**
- A failing search request produces a clear inline error after a loading state
- Search Settings remain populated after the error

**Fail:**
- The request succeeds when it was expected to fail (indicates the confirmed failure input is no longer valid and must be re-confirmed)
- No error is shown, or the error is unclear
- Search Settings are cleared after the error
