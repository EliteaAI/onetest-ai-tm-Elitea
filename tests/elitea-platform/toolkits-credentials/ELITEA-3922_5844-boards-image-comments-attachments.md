---
id: ELITEA-3922
title: "[EliteaAI/elitea_issues#5844] ADO Boards: Same Image in Comments & Attachments"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-3922: ADO Boards — Same Image Across Comments & Work Item Attachments

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify cache reuse across different Boards entry points (get_comments vs get_work_item) within same toolkit session.

## Preconditions

- ADO toolkit configured with `process_images: true`
- Work item has:
  - Image attachment in comments (via get_comments path)
  - Same image attached to work item body/attachments (via get_work_item path)
- Same toolkit session (no restart)
- LLM/tool logs visible

## Test Data

| Entry Point | Image Source | URL |
|-------------|--------------|-----|
| get_comments | Comment attachment | /attachments/image.jpg |
| get_work_item | Work item attachment | /attachments/image.jpg |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_comments(..., process_images=true)` for work item with image in comment. | Comments retrieved; image described. |
| 2 | Check logs: verify first LLM vision call for image. | LLM called; description generated. |
| 3 | Call `get_work_item(..., parse_attachments=true, process_images=true)` where same image is attached to work item. | Work item retrieved. |
| 4 | Verify image description in work item is present. | Image described in work item attachment. |
| 5 | Check logs: verify NO second LLM vision call for same image. | Same image reuses cached description; 1 LLM call total. |
| 6 | Confirm descriptions are identical. | Description from get_comments matches get_work_item. |
| 7 | Verify both paths return correct content. | Both calls include descriptions; content valid. |

## Expected Final State

- Second path reuses cached description
- No duplicate LLM call for same image in same session
- Descriptions consistent across entry points
- Cache shared across get_comments and get_work_item
- Correct content output from both paths

## Pass/Fail Criteria

**Pass:** Cache reused across paths; 1 LLM call; descriptions match; content valid.  
**Fail:** Separate LLM calls; descriptions differ; cache not shared; content errors.
