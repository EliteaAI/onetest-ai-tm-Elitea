---
id: ELITEA-2984
title: "ADO Work Item Text Search – Highlight text Is HTML-Stripped to Plain Text and Truncated to 200 Characters"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2984: ADO Work Item Text Search – Highlight text Is HTML-Stripped to Plain Text and Truncated to 200 Characters

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify each highlight `text` value contains no HTML markup and is at most 200 characters.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- At least one matching work item has HTML markup in a highlighted field (e.g. an HTML-formatted description) and a match producing a long highlight snippet.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `include_highlights=true` against a query matching a work item with HTML-formatted field content | Call succeeds |
| 2 | Inspect the highlight `text` for that field | No HTML tags/entities present — plain text only |
| 3 | Measure the length of every highlight `text` value across all highlighted results | Every value is ≤200 characters |

---

## Expected Final State

Highlight snippets are always clean plain text within the 200-character bound, regardless of source formatting or match length.

---

## Pass/Fail Criteria

**Pass:** All highlight `text` values are HTML-free and ≤200 characters.
**Fail:** Any highlight `text` contains HTML markup, or exceeds 200 characters.
