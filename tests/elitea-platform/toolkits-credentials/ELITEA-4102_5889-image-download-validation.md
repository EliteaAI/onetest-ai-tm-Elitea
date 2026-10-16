---
id: ELITEA-4102
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Image Download & Binary Validation"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4102: ADO Toolkit — Image Download & Binary Validation

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that images are successfully downloaded from ADO URLs using existing credentials and binary validation is performed.

## Preconditions

- ADO toolkit configured with valid credentials (OAuth or PAT)
- `process_images: true` enabled
- ADO work item with comments containing image URLs
- Image URLs are accessible and valid
- Network connectivity available

## Test Data

| Scenario | URL | Expected Status |
|----------|-----|-----------------|
| Valid image | ADO attachment URL | 200 OK |
| Inaccessible image | Non-existent URL | Error (graceful) |
| Expired token | Old credential URL | Error (graceful) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments with valid accessible image URLs. | Tool initiates HTTP download for each image URL. |
| 2 | Verify HTTP request uses existing ADO credentials from toolkit config. | Images downloaded successfully with 200 response. |
| 3 | Verify downloaded binary is validated (non-empty, correct format). | Binary header/magic bytes match image format (JPEG, PNG, etc.). |
| 4 | Verify very small binary (0 bytes) is rejected. | Empty binary treated as invalid; error message returned. |
| 5 | Verify very large image (>100MB) is handled. | Download initiated; size limit enforced if applicable. |
| 6 | Test with inaccessible URL (404, 403). | Graceful error returned; processing continues with other images. |
| 7 | Test with network timeout (slow server). | Timeout error returned gracefully; doesn't block other images. |
| 8 | Verify authentication error (expired token). | Clear error message; tool suggests re-authentication. |

## Expected Final State

- Images downloaded successfully using ADO credentials
- Binary validated (non-empty, correct format)
- Inaccessible URLs return graceful errors
- Processing continues despite individual image failures
- Network timeouts handled gracefully
- Authentication errors clearly identified

## Pass/Fail Criteria

**Pass:** Valid images downloaded; binary validated; inaccessible/timeout errors handled gracefully.  
**Fail:** Download fails with valid URLs; invalid binary accepted; errors block processing; auth issues not identified.
