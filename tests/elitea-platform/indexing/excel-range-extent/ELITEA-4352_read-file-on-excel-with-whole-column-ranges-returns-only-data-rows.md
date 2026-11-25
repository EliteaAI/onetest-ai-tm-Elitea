---
id: ELITEA-4352
title: "Agent read_file on an Excel file with whole-column ranges returns only the data rows quickly"
priority: medium
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, feat:agents, issue:7286, excel, p2]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4352: Agent read_file on an Excel file with whole-column ranges returns only the data rows quickly

**Module:** indexing · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that reading an `.xlsx` file through an agent's Artifact toolkit (`read_file`) also ignores the parts of whole-column merges and hyperlinks below the data. The #7286 fix moved `read_file` onto the same Excel reader that indexing uses, so both must behave the same way.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with bucket **B** containing `link_whole_column.xlsx` and `merge_whole_column.xlsx` (see ELITEA-4349 and ELITEA-4350).
- An agent **A** in P with toolkit T attached, including the `read_file` tool.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat with agent A and send: `Read the file link_whole_column.xlsx from the bucket and show me its content exactly.` | The agent calls `read_file` for `link_whole_column.xlsx`. |
| 2 | Expand the `read_file` tool call in the chat and check its output. | The tool finishes within a few seconds. The output has 5 rows (`name | value`, `row 1 | 1` … `row 4 | 4`). It does not contain thousands of empty rows, and does not fail with a size or limit error. |
| 3 | Send: `Now read merge_whole_column.xlsx the same way.` | The agent calls `read_file` for `merge_whole_column.xlsx`. |
| 4 | Expand the tool call and check its output. | The tool finishes within a few seconds and returns the same 5 rows only. |

---

## Expected Final State

`read_file` returns only the 5 real rows for both files, quickly and without errors.

---

## Pass/Fail Criteria

**Pass:**
- Both `read_file` calls finish within a few seconds and return exactly the 5 data rows.

**Fail:**
- A tool call runs for a long time, times out, or returns thousands of empty rows.
- A tool call fails with a "file too large" or row-limit error for a 5 KB file.
