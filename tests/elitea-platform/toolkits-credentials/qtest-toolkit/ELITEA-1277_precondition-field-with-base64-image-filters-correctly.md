---
id: ELITEA-1277
title: "Precondition field with base64 image filters correctly"
priority: critical
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [rca:missing-functionality, issue:4531, int:qtest, r-2.0.2, eng:sdk]
requirements: [EliteaAI/elitea_issues#4531]
---
# ELITEA-1277: Precondition field with base64 image filters correctly

**Module:** Qtest Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a qTest test case with base64 image data in the Precondition field is retrieved via the toolkit with `extract_images=True`, the base64 data is correctly filtered and not leaked in the response.

**Coverage:**
- Base64 image data in Precondition field is filtered when `extract_images=True`
- `_process_image()` method is correctly applied to Precondition field
- No base64 data leakage in toolkit response
- Precondition field processing matches Description field behavior

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- qTest toolkit is configured with valid credentials
- Test environment has access to qTest instance
- Browser: Chrome/Edge latest

## Test Data

- qTest test case with Precondition field containing: `<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUA..." alt="test image"/>`
- qTest project ID and test case ID
- `extract_images` parameter set to `True`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a qTest test case via qTest UI with Precondition field containing HTML with embedded base64 image: <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUA..." alt="test image"/> | Test case is created successfully in qTest with the base64 image in Precondition field. |
| 2 | In ELITEA, configure an Agent with qTest toolkit and invoke get_test_case with the test case ID and extract_images=True parameter. | Toolkit executes successfully and returns test case data. |
| 3 | Inspect the returned Precondition field in the response. | Precondition field does NOT contain the full base64 string data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUA.... Base64 image data is filtered or replaced with a placeholder/reference. |
| 4 | Verify no base64 data appears anywhere in the toolkit response payload. | No base64 string matching data:image/...;base64,... is present in the entire response. |

## Expected Final State

No base64 string matching data:image/...;base64,... is present in the entire response.

## Pass/Fail Criteria

**Pass:**
- Precondition field is returned without base64 image data
- `_process_image()` correctly filters base64 from Precondition field
- No base64 leakage in response payload
- Toolkit execution completes without errors

**Fail:**
- Full base64 string appears in Precondition field
- Base64 data leaks into response payload
- Toolkit throws an exception or error
- Precondition field is missing or corrupted
