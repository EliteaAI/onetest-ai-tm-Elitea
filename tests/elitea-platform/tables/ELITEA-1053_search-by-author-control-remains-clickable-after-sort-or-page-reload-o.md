---
id: ELITEA-1053
title: "Search by Author Control Remains Clickable After Sort or Page Reload on Single-Author Batch"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3899]
---
# ELITEA-1053: Search by Author Control Remains Clickable After Sort or Page Reload on Single-Author Batch

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Search by Author control remains clickable and functional after sorting is applied or the page is reloaded when the visible batch contains items from only a single author.

**Coverage:**
- Search by Author control is interactive before any sort is applied
- Search by Author control remains clickable immediately after an Authors column sort is applied
- Search by Author control remains clickable after a full page reload while sort is active and first batch is single-author
- No frozen, disabled, or unresponsive state is triggered by the sort+single-author combination
- No JavaScript console errors related to the author filter control

## Preconditions

- User is logged in to {{base_url}}
- A project is selected that contains an entity table (Agents, Pipelines, Credentials, Toolkits, MCPs, or Apps) where one author owns enough items to fill the entire first page
- Table View is active for the selected entity
- Browser DevTools console is open to monitor for JS errors

## Test Data

- Entity table: Agents (or any table with sufficient single-author data)
- Rows-per-page value: 10 (to ensure first batch shows only one author's items)
- Author name to use: any project member who owns ≥ 10 items in the table
- Sort column: Authors (ascending)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents table (or chosen entity) and switch to Table View. | Table View is active and rows are displayed. |
| 2 | Set rows-per-page to 10 using the pagination control at the bottom of the table. | Table displays 10 rows. If all 10 belong to a single author, pre-condition is satisfied. |
| 3 | Locate the Search by Author control (author filter/search) and click it. | The control responds — a dropdown, input field, or filter panel opens. Control is fully interactive. |
| 4 | Close/dismiss the Search by Author control. Click the Authors column header to apply ascending sort. | Table re-renders sorted by author name (A→Z). An ascending sort indicator appears on the Authors column header. |
| 5 | With the sort active, click the Search by Author control. | The control responds and opens normally — it is not frozen, disabled, or unresponsive. |
| 6 | Close/dismiss the control. Without clearing the sort, reload the page (press F5 or use the browser refresh button). | Page reloads. Table View re-displays with the single-author batch still visible on page 1. |
| 7 | After the page has fully loaded, click the Search by Author control. | The control responds and opens normally — it is not frozen, disabled, or unresponsive after the reload. |
| 8 | Check the browser DevTools console for any JavaScript errors. | No JS errors related to the author filter control or sort state are logged. |

## Expected Final State

No JS errors related to the author filter control or sort state are logged.

## Pass/Fail Criteria

**Pass:**
- Search by Author control opens and responds in all three states: before sort, after sort, and after page reload
- No frozen, stuck, or disabled state is observed on the control at any point
- No JavaScript errors appear in the browser console

**Fail:**
- Search by Author control becomes unclickable or unresponsive after sort is applied
- Search by Author control becomes unclickable or unresponsive after page reload when single-author batch is shown
- Control appears visually enabled but does not react to clicks
- JavaScript errors related to author filter or sort state are logged in the console
