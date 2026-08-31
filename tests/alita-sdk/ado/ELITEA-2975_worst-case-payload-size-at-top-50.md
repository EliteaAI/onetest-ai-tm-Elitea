---
id: ELITEA-2975
title: "ADO Work Item Text Search – Worst-Case Payload Size at top=50 With Adversarially Long Field Values"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, inconclusive]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2975: ADO Work Item Text Search – Worst-Case Payload Size at top=50 With Adversarially Long Field Values

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the response payload at `top=50` stays within a reasonable, documented size bound even when titles and assignee display names are unusually long. **Status: previously untested with typical-length data only — needs adversarial-length test data.**

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- At least 50 matching work items exist, ideally including several with very long titles (e.g. 250+ characters) and long assignee display names.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Identify or create work items with unusually long titles/assignee names matching a common query term | Test data prepared |
| 2 | Call `search_work_items_by_text` with `top=50` against that query | Call succeeds |
| 3 | Measure the serialized response payload size | Payload size stays within a reasonable bound (no field is unbounded/untruncated in a way that causes multi-MB responses) |

---

## Expected Final State

Even with long field values, the 50-result response remains a bounded, predictable size.

---

## Pass/Fail Criteria

**Pass:** Payload size at `top=50` with long field values stays within a sane bound (no runaway growth from unbounded title/name length).
**Fail:** A small number of long-title/long-name work items cause disproportionate payload growth, suggesting no field-length cap exists.
