---
id: ELITEA-2289
title: "VSCode download icon generates a downloadable configuration file"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2289: VSCode download icon generates a downloadable configuration file

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that VSCode download icon generates a downloadable configuration file. Success is confirmed when verify the downloaded file is not empty and contains valid configuration content referencing the correct token and server url.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Personal Tokens with at least one token | Target page/section loads successfully. |
| 2 | Click the VSCode (blue) icon in the Actions column of a token row | Control responds; expected next state is shown. |
| 3 | Verify a file is downloaded | Condition holds as described. |
| 4 | Verify the downloaded file is not empty and contains valid configuration content referencing the correct token and server URL | Condition holds as described. |

---

## Expected Final State

Verify the downloaded file is not empty and contains valid configuration content referencing the correct token and server URL.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: VSCode download icon generates a downloadable configuration file.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
