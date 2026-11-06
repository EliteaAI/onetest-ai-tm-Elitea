---
id: ELITEA-4350
title: "A merge applied to a whole Excel column does not expand the indexed sheet beyond its data rows"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, p1]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4350: A merge applied to a whole Excel column does not expand the indexed sheet beyond its data rows

**Module:** indexing · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that when an `.xlsx` file has a merged range covering a whole column, indexing it produces chunks only for the rows that hold data. Before the fix, the indexer wrote one empty line for each of the 1,048,576 rows the merge covered.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured.
- Test file `merge_whole_column.xlsx` (about 5 KB). It has a sheet **Data** with 5 rows (`name | value`, `row 1 | 1` … `row 4 | 4`) and one merged range `C1:C1048576`.

---

## Test Data

| File | Real rows | Range in the sheet XML | Before the fix |
|---|---|---|---|
| `merge_whole_column.xlsx` | 5 | merge `C1:C1048576` | 1,048,576 lines, 7.3 M chars, ~23 s just to read |

**How to create the file in Excel:** type the 5 rows in A1:B5. Click the **C** column header to select the whole column, choose **Home → Merge & Center → Merge Cells**, and save as `.xlsx`.

The file can also be generated with the `make_workbooks.py` script attached to EliteaAI/elitea_issues#7286.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `merge_whole_column.xlsx` to bucket B of toolkit T. | The file appears in the bucket, about 5 KB in size. |
| 2 | Open T, go to the **Indexes** tab and click **+ Create Index**. Enter the suffix `xlrange2`, leave the default chunking settings and click **Index**. | The index starts and its status is **In Progress**. |
| 3 | Wait for indexing to finish, and note how long it took. | Status becomes **Completed** within about 1 minute. |
| 4 | Open the **History** tab for the index and check the summary. | `merge_whole_column.xlsx` is listed as indexed, with a small chunk count (1 with default settings). |
| 5 | On the index, open **Search** and search for `row 2`. | A result from `merge_whole_column.xlsx` is returned that contains `row 2 | 2`. The result text has 5 lines, not many empty `| |` lines. |

---

## Expected Final State

The index for `merge_whole_column.xlsx` has completed and contains only the 5 real rows. The whole-column merge did not add empty rows.

---

## Pass/Fail Criteria

**Pass:**
- Indexing completes within about 1 minute.
- The search in step 5 returns the 5 real rows only.

**Fail:**
- Indexing stays **In Progress** for many minutes, or ends **Stopped** / **Failed**.
- The indexed text contains thousands of empty `| |` lines.
