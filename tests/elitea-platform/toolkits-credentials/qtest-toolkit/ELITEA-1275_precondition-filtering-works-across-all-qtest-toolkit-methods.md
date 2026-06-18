---
id: ELITEA-1275
title: "Precondition filtering works across all qTest toolkit methods"
priority: high
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [rca:missing-functionality, issue:4531, int:qtest, r-2.0.2, eng:sdk]
requirements: [EliteaAI/elitea_issues#4531]
---
# ELITEA-1275: Precondition filtering works across all qTest toolkit methods

**Module:** Qtest Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that Precondition field base64 image filtering is applied consistently across all toolkit methods that return test case data (`get_test_case`, `search_test_cases`, and any other retrieval methods).

**Coverage:**
- `get_test_case` filters Precondition field base64 images
- `search_test_cases` filters Precondition field base64 images
- Filtering behavior is consistent across all methods
- No method-specific discrepancies

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- qTest toolkit is configured with valid credentials
- Test environment has access to qTest instance
- Browser: Chrome/Edge latest

## Test Data

- qTest test case with Precondition field containing: `<img src="data:image/png;base64,iVBORw0..." alt="precondition"/>`
- qTest project ID and test case ID
- Search query matching the test case
- `extract_images` parameter set to `True` for all methods

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a qTest test case via qTest UI with Precondition field containing base64 image: <img src="data:image/png;base64,iVBORw0..." alt="precondition"/> | Test case is created successfully in qTest. |
| 2 | Invoke get_test_case with the test case ID and extract_images=True. | Precondition field is returned WITHOUT base64 data. Image is filtered correctly. |
| 3 | Invoke search_test_cases with a query matching the test case and extract_images=True. | Search results include the test case. Precondition field in search results does NOT contain base64 data. |
| 4 | Compare Precondition field output from both methods. | Both get_test_case and search_test_cases return identical Precondition field content with base64 filtered. Filtering is consistent. |

## Expected Final State

Both get_test_case and search_test_cases return identical Precondition field content with base64 filtered. Filtering is consistent.

## Pass/Fail Criteria

**Pass:**
- Precondition base64 filtering works in `get_test_case`
- Precondition base64 filtering works in `search_test_cases`
- Filtering behavior is identical across all methods
- No method-specific discrepancies

**Fail:**
- Base64 data appears in Precondition from any method
- Filtering is inconsistent between methods
- One method filters while another doesn't
- Toolkit throws errors in any method
