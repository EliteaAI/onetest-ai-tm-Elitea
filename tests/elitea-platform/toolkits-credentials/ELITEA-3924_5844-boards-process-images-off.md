---
id: ELITEA-3924
title: "[EliteaAI/elitea_issues#5844] ADO Boards: process_images=false (Unchanged Behavior)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-3924: ADO Boards — process_images=false (Backward Compatibility)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that existing behavior is unchanged when image processing is disabled.

## Preconditions

- ADO toolkit available
- Work items with comments/attachments containing images
- process_images explicitly set to false OR using default (false)

## Test Data

| Setting | Value |
|---------|-------|
| get_comments: process_images | false |
| get_work_item: parse_attachments | true |
| get_work_item: process_images | false |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_comments(..., process_images=false)`. | Comments retrieved. |
| 2 | Verify no image-description generation. | No LLM vision calls made. |
| 3 | Verify raw content behavior remains unchanged. | Attachments/images returned as-is (no descriptions added). |
| 4 | Call `get_work_item(..., parse_attachments=true, process_images=false)`. | Work item retrieved. |
| 5 | Verify no image-description generation. | No LLM vision calls. |
| 6 | Verify attachments returned without processing. | Raw attachment data unchanged. |
| 7 | Confirm enhancement did not alter the off-path. | Behavior identical to pre-enhancement. |
| 8 | Verify no performance impact when feature disabled. | Processing time unaffected. |

## Expected Final State

- No image-description generation when disabled
- Raw content behavior unchanged
- No LLM vision calls
- Pre-enhancement behavior preserved
- No performance impact

## Pass/Fail Criteria

**Pass:** No image processing; raw behavior; no LLM calls; pre-enhancement identical.  
**Fail:** Image processing occurs; behavior changed; LLM calls made; performance degraded.
