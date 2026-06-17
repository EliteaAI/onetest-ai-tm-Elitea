---
id: ELITEA-1279
title: "Precondition field respects extract_images=False parameter"
priority: high
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [rca:missing-functionality, issue:4531, int:qtest, r-2.0.2, eng:sdk]
requirements: [EliteaAI/elitea_issues#4531]
---
# ELITEA-1279: Precondition field respects extract_images=False parameter

**Module:** Qtest Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that when `extract_images=False` is set, the Precondition field base64 image data is NOT filtered and is returned as-is in the response.

**Coverage:**
- `extract_images=False` parameter is respected for Precondition field
- Base64 data is NOT filtered when parameter is False
- Parameter behavior is consistent across all fields
- No unintended filtering occurs

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- qTest toolkit is configured with valid credentials
- Test environment has access to qTest instance
- Browser: Chrome/Edge latest

## Test Data

- qTest test case with Precondition field containing: `<img src="data:image/png;base64,iVBORw0KGgo..." alt="precondition image"/>`
- qTest project ID and test case ID
- `extract_images` parameter set to `False`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a qTest test case via qTest UI with Precondition field containing base64 image: <img src="data:image/png;base64,iVBORw0KGgo..." alt="precondition image"/> | Test case is created successfully in qTest. |
| 2 | In ELITEA, invoke get_test_case with the test case ID and extract_images=False parameter. | Toolkit executes successfully. |
| 3 | Inspect the returned Precondition field. | Precondition field CONTAINS the full base64 image string exactly as stored in qTest. No filtering has occurred. |
| 4 | Verify the base64 string is intact and complete. | Full base64 string data:image/png;base64,iVBORw0KGgo... is present in Precondition field. |

## Expected Final State

Full base64 string data:image/png;base64,iVBORw0KGgo... is present in Precondition field.

## Pass/Fail Criteria

**Pass:**
- `extract_images=False` prevents filtering in Precondition field
- Full base64 string is returned unmodified
- Parameter behavior is consistent
- Toolkit execution completes without errors

**Fail:**
- Base64 data is filtered despite `extract_images=False`
- Precondition field is missing or corrupted
- Parameter has no effect on filtering
- Toolkit throws an error
