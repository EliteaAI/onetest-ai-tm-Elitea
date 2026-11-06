---
id: ELITEA-4351
title: "A realistic Excel workbook with a whole-column link and merged cells indexes only its data rows on every sheet"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, p1]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4351: A realistic Excel workbook with a whole-column link and merged cells indexes only its data rows on every sheet

**Module:** indexing · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that a normal-looking workbook saved by Microsoft Excel, with a hyperlink placed on a whole column, indexes correctly. Only the real rows should be indexed on each sheet, and the data in them should stay searchable. This is the case from EliteaAI/elitea_issues#7286: Excel itself keeps a whole-column link when saving, so real user files can hit this.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured.
- Microsoft Excel, to create the test file.

---

## Test Data

Create `contacts_example.xlsx` in Microsoft Excel with two sheets:

| Sheet | Content |
|---|---|
| **Contacts** | Header row `Name | Email | Region | Phone | Directory`, then 10 people, e.g. `Anna Petrosyan | anna.p@example.com | EMEA | +374 10 000001`. Merge `C2:C11` (Region) after typing `EMEA` in C2. Select the whole **E** column and insert one link to cell `A1` of sheet **Directory** (Insert → Link → Place in This Document), with the text `Open directory` in E2. |
| **Directory** | `Team | Lead`, `Sales | Anna Petrosyan`, `Support | Ben Carter`. No merges or links. |

Before the fix, this file (about 6 KB) was read as 1,048,576 lines and 34.6 M characters on **Contacts**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `contacts_example.xlsx` to bucket B of toolkit T. | The file appears in the bucket. |
| 2 | Open T, go to the **Indexes** tab and click **+ Create Index**. Enter the suffix `xlrange3`, leave the default chunking settings and click **Index**. | The index starts with status **In Progress**. |
| 3 | Wait for indexing to finish, and note how long it took. | Status becomes **Completed** within about 1 minute. |
| 4 | Open the **History** tab and check the summary. | `contacts_example.xlsx` is listed as indexed. There is one chunk per sheet with default settings: 2 in total, not thousands. |
| 5 | Search for `Anna Petrosyan`. | Results come back from both sheets: the **Contacts** row with her email and phone, and the **Directory** row `Sales | Anna Petrosyan`. |
| 6 | Search for `Julia Rossi`. | The **Contacts** row for Julia Rossi is returned. The data in the last real row is indexed. |
| 7 | Search for `Open directory`. | The **Contacts** chunk is returned, and in it the link appears only on rows 2–11, not on empty rows below the table. |

---

## Expected Final State

Both sheets are indexed with only their real rows. Contact data on both sheets is searchable, and the whole-column link did not add filler rows.

---

## Pass/Fail Criteria

**Pass:**
- Indexing completes within about 1 minute.
- Steps 5 and 6 return the correct rows from the right sheets.
- No chunk contains empty rows below the table.

**Fail:**
- Indexing stays **In Progress** for many minutes, or ends **Stopped** / **Failed**.
- The **Contacts** chunk contains empty rows below the table with only the link text.
- Data from the **Directory** sheet or the last contact row is missing from search.
