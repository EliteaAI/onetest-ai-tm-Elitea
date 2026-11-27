---
id: ELITEA-5019
title: "Verify Toolkits & Indexes, MCPs and Credentials pages: no tabs, hidden filter panel and direct Add"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7569]
---
# ELITEA-5019: Verify Toolkits & Indexes, MCPs and Credentials pages: no tabs, hidden filter panel and direct Add

## Preconditions

- User is logged in to `{{base_url}}`
- A private project and a team project with toolkits and MCPs of different types (some in folders) and some credentials

## Test Data

| Section | Filters behind the filter icon | Search placeholder |
|---------|-------------------------------|--------------------|
| Toolkits & Indexes | Folders, toolkit Types | Search toolkits & indexes |
| MCPs | Folders, MCP Types (e.g. Local, Remote) | Search MCPs |
| Credentials | Existing page — no new filters | Existing |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Toolkits & Indexes** from Explore | Correct title; no Yours / Team / Discover tabs; Card view by default |
| 2 | Look at the page without clicking anything | **Folders** and **Types** are not visible |
| 3 | Click the filter icon in the search field | A panel opens on the right with the filters from the Test Data |
| 4 | Select a type, then click the filter icon again | The list shows only that type; the panel hides and the filter stays applied |
| 5 | Enter a search term, switch to Table view and back | The search and filters are kept |
| 6 | Repeat steps 1–5 on **MCPs** | Same behaviour with the MCP filters |
| 7 | Open **Credentials** | The page, list and search work as before; no Folders or Types filters and no new views |
| 8 | Click **+ Add** on each of the three pages | A direct button with no dropdown, no Import and no Build with AI; it opens the existing creation flow for that entity |
| 9 | Switch to the team project and open each page again | Content refreshes for that project; still no tabs |

## Expected Final State

All creation dialogs are closed and nothing was created.

## Pass/Fail Criteria

**Pass:**
- No tabs on any of the three pages
- Folders and Types are hidden until the filter icon is clicked and toggle with it
- **+ Add** opens the correct creation flow directly; Credentials is unchanged

**Fail:**
- Filters are visible on page load or don't toggle
- Tabs appear, or **+ Add** shows a dropdown or extra options
- Credentials gets new filters or views
