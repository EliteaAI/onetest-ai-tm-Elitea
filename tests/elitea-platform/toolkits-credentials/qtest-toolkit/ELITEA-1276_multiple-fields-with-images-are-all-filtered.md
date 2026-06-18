---
id: ELITEA-1276
title: "Multiple fields with images are all filtered"
priority: medium
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [rca:missing-functionality, issue:4531, int:qtest, r-2.0.2, eng:sdk]
requirements: [EliteaAI/elitea_issues#4531]
---
# ELITEA-1276: Multiple fields with images are all filtered

**Module:** Qtest Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a qTest test case contains base64 images in multiple fields (Description, Precondition, Test Steps), all base64 images are filtered correctly without cross-field contamination or missed filtering.

**Coverage:**
- Description field base64 filtering works
- Precondition field base64 filtering works
- Test Steps base64 filtering works (if applicable)
- No cross-field contamination (image from one field leaking into another)
- All fields are processed independently and correctly

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- qTest toolkit is configured with valid credentials
- Test environment has access to qTest instance
- Browser: Chrome/Edge latest

## Test Data

- qTest test case with:
  - Description: `<img src="data:image/png;base64,AAAA..." alt="desc"/>`
  - Precondition: `<img src="data:image/jpeg;base64,BBBB..." alt="precond"/>`
  - Test Step description: `<img src="data:image/gif;base64,CCCC..." alt="step"/>`
- qTest project ID and test case ID
- `extract_images` parameter set to `True`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a qTest test case via qTest UI with base64 images in Description, Precondition, and at least one Test Step description field. | Test case is created successfully with all base64 images in their respective fields. |
| 2 | In ELITEA, invoke get_test_case with the test case ID and extract_images=True. | Toolkit executes successfully and returns test case data. |
| 3 | Inspect the returned Description field. | Description field does NOT contain base64 string AAAA.... Image is filtered. |
| 4 | Inspect the returned Precondition field. | Precondition field does NOT contain base64 string BBBB.... Image is filtered. |
| 5 | Inspect the returned Test Steps field (if base64 filtering applies to steps). | Test Step description does NOT contain base64 string CCCC... (if filtering is implemented for steps). |
| 6 | Verify no base64 data appears anywhere in the response payload. | No base64 strings matching data:image/...;base64,... are present in any field. |

## Expected Final State

No base64 strings matching data:image/...;base64,... are present in any field.

## Pass/Fail Criteria

**Pass:**
- All base64 images are filtered from Description, Precondition, and Test Steps
- No cross-field contamination
- Each field is processed independently
- No base64 leakage in response payload

**Fail:**
- Base64 data appears in any field
- Cross-field contamination occurs (image from one field leaks into another)
- Inconsistent filtering across fields
- Toolkit throws an error
