---
id: ELITEA-0992
title: "Secret Masking/Unmasking Functionality"
priority: high
type: functional
module: secrets
status: draft
execution_type: manual
tags: [masking-unmasking, R-2.0.1, secrets]
requirements: [ProjectAlita/projectalita.github.io#3578]
---
# ELITEA-0992: Secret Masking/Unmasking Functionality

**Module:** Secrets · **Priority:** High · **Type:** Functional

**Objective:** Ensure the masking/unmasking control correctly toggles secret values without errors.

## Preconditions

- User is logged in
- Secret management UI is accessible
- At least one secret (e.g., "sampleText") is already successfully created

## Test Data

| Secret Value | Type |
| ------------- | ----- |
| "sampleText" | Normal value |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the show/hide toggle for the secret. | UI toggles the display between masked/unmasked correctly. Value is displayed as expected in each state. |
| 2 | Repeat toggle multiple times. | UI consistently toggles correctly. No errors or broken display. |

## Expected Final State

UI consistently toggles correctly. No errors or broken display.

## Pass/Fail Criteria

Pass Criteria
- UI correctly toggles masked/unmasked state
- Behavior is consistent across multiple toggles
- No errors or failed requests
