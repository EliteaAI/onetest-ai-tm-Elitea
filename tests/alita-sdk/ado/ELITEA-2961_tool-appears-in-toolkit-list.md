---
id: ELITEA-2961
title: "ADO Work Item Text Search – Tool Appears in Toolkit's Available Tools List"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2961: ADO Work Item Text Search – Tool Appears in Toolkit's Available Tools List

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify `search_work_items_by_text` is listed as an available tool on the ADO Board/Work Item toolkit, alongside the existing `search_work_items` WIQL tool.

---

## Preconditions

- ADO Board (Work Item) toolkit is configured with valid credentials and a project.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open an Agent/Chat with the ADO Board toolkit attached and list its available tools | `search_work_items_by_text` appears in the tool list |
| 2 | Confirm `search_work_items` (WIQL) is also still present | Both tools are listed side by side, neither replaces the other |

---

## Expected Final State

The toolkit exposes both the existing WIQL search tool and the new text search tool.

---

## Pass/Fail Criteria

**Pass:** `search_work_items_by_text` is listed and `search_work_items` is unaffected.
**Fail:** The new tool is missing, mislabeled, or its presence hides/breaks the existing WIQL tool.
