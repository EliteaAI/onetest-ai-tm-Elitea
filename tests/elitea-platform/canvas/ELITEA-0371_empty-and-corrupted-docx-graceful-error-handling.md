---
id: ELITEA-0371
title: "Empty and Corrupted DOCX — Graceful Error Handling"
priority: medium
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0371: Empty and Corrupted DOCX — Graceful Error Handling

**Module:** Canvas · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attempting to open an empty, corrupted, or unsupported Strict Open XML `.docx` file in Canvas results in a graceful error — not a crash or blank modal.

**Coverage (parametrized):**
- Empty DOCX (0 bytes) — graceful empty state or clear error
- Corrupted file: non-Word binary renamed to `.docx` — clear error message

## Preconditions

- Logged in to {{base_url}}
- Three test files uploaded to bucket `test-docx-bucket`:
  - `empty.docx` (0 bytes)
  - `corrupt.docx` (e.g. a `.png` file renamed to `.docx`)

## Test Data

- `empty.docx` — 0 bytes
- `corrupt.docx` — binary non-Word file with `.docx` extension

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the eye icon on `empty.docx` in the Artifacts bucket | Canvas opens with a graceful empty state or a clear, user-friendly error message — no unhandled JS crash or blank white modal |
| 2 | Click the eye icon on `corrupt.docx` | Canvas displays a clear error message indicating the file cannot be read — no crash or raw stack trace |

## Expected Final State

Canvas displays a clear error message indicating the file cannot be read — no crash or raw stack trace

## Pass/Fail Criteria

**Pass:**
- All cases show a user-friendly message or graceful empty state
- No browser crash, blank modal, or raw JS/stack trace is exposed

**Fail:**
- Any case causes a browser or application crash
- A blank/white modal is shown with no error message
- Raw error stack trace is exposed to the user
