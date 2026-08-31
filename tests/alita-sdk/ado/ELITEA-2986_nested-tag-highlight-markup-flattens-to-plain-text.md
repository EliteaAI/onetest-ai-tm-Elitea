---
id: ELITEA-2986
title: "ADO Work Item Text Search – Nested-Tag Highlight Markup Flattens to Clean Plain Text"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, inconclusive]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2986: ADO Work Item Text Search – Nested-Tag Highlight Markup Flattens to Clean Plain Text

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when the Azure DevOps Search API returns highlight markup with nested tags (e.g. `<div><b>term</b></div>`), the tool's HTML-stripping produces clean plain text with no residual tag fragments or lost spacing. **Status: previously untested — no query during exploratory testing produced nested markup; needs a targeted repro.**

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A work item field is identified/constructed where a match is likely to be wrapped in nested HTML (e.g. a rich-text description field containing the search term inside a formatted block like a bolded list item).

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Identify a work item and query combination likely to produce nested-tag highlight markup from the search API | Candidate found (may require inspecting raw ADO Search API output if directly reachable) |
| 2 | Call `search_work_items_by_text` with `include_highlights=true` against that query | Call succeeds |
| 3 | Inspect the resulting highlight `text` | No tag fragments (`<`, `>`, tag names) remain; text reads naturally with appropriate spacing where tags were removed |

---

## Expected Final State

Highlight stripping handles nested markup correctly, with no leaked tags or word-mashing where tags were removed.

---

## Pass/Fail Criteria

**Pass:** Nested markup is fully and cleanly stripped, text reads correctly.
**Fail:** Any tag fragment remains, or words are incorrectly mashed together after stripping.
