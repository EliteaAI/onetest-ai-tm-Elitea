---
id: ELITEA-4349
title: "A hyperlink applied to a whole Excel column does not expand the indexed sheet beyond its data rows"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, p1]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4349: A hyperlink applied to a whole Excel column does not expand the indexed sheet beyond its data rows

**Module:** indexing · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that when an `.xlsx` file has one hyperlink applied to a whole column, indexing it produces chunks only for the rows that hold data. Before the fix, the indexer wrote one line for each of the 1,048,576 rows in the link's range and filled every empty cell with the link text. A 5 KB file produced about 26 million characters and indexing ran for a very long time.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured, so indexing can run.
- Test file `link_whole_column.xlsx` (about 5 KB). It has a sheet **Data** with 5 rows (`name | value`, `row 1 | 1` … `row 4 | 4`), and one hyperlink to `Data!A1` on the range `D1:D1048576`. See **Test Data** for how to create it.

---

## Test Data

| File | Real rows | Range in the sheet XML | Before the fix |
|---|---|---|---|
| `link_whole_column.xlsx` | 5 | hyperlink `D1:D1048576` → `Data!A1` | 1,048,576 lines, 26.2 M chars, ~47 s just to read |

**How to create the file in Excel:** type the 5 rows in A1:B5. Click the **D** column header to select the whole column, choose **Insert → Link → Place in This Document**, pick cell `A1` of sheet **Data**, and save as `.xlsx`.

The same file can also be generated with the `make_workbooks.py` script attached to EliteaAI/elitea_issues#7286.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `link_whole_column.xlsx` to bucket B of toolkit T. | The file appears in the bucket, about 5 KB in size. |
| 2 | Open T, go to the **Indexes** tab and click **+ Create Index**. Enter the suffix `xlrange1`, leave the default chunking settings and click **Index**. | The index starts and its status is **In Progress**. |
| 3 | Wait for indexing to finish, and note how long it took. | Status becomes **Completed** within about 1 minute. It does not stay **In Progress** for a long time, and does not end as **Stopped** or **Failed**. |
| 4 | Open the **History** tab for the index and check the summary. | `link_whole_column.xlsx` is listed as indexed. The chunk count is small (1 with default settings), not thousands. |
| 5 | On the index, open **Search** and search for `row 3`. | A result from `link_whole_column.xlsx` is returned that contains `row 3 | 3`. |
| 6 | Search for `Data!A1`. | No more than a few results are returned, all from the 5 real rows. Results made only of empty cells and `Data!A1` link text are not returned. |

---

## Expected Final State

The index for `link_whole_column.xlsx` has completed and contains only the 5 real rows of the sheet. The whole-column hyperlink did not add empty rows.

---

## Pass/Fail Criteria

**Pass:**
- Indexing completes within about 1 minute.
- The search in step 5 returns the row data.
- The search in step 6 does not return filler chunks of empty cells with the link text.

**Fail:**
- Indexing stays **In Progress** for many minutes, or ends **Stopped** / **Failed**.
- The index holds thousands of chunks, or search results consist of `| | | [Data!A1](...)` lines.
- The indexer pod restarts or runs out of memory during the run.
