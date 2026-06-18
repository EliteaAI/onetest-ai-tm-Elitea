---
id: ELITEA-1683
title: "XR04 - Create Generic Test"
priority: high
type: functional
module: xray
status: draft
execution_type: automated
automation_test_id:
  - XR04
tags: [integration, generic, create, xray]
requirements: []
---
# ELITEA-1683: XR04 - Create Generic Test

**Module:** Xray · **Priority:** High · **Type:** Functional

**Objective:** Verify the Xray 'create_test' tool creates a generic test successfully

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create generic test without steps | Test is created successfully |

## Expected Final State

Test is created successfully

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
