---
id: ELITEA-5022
title: "Section pages: tabs by project type, hidden filter panel and Add per section"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7565, EliteaAI/elitea_issues#7569, EliteaAI/elitea_issues#7571, EliteaAI/elitea_issues#7560]
---
# ELITEA-5022: Section pages: tabs by project type, hidden filter panel and Add per section

## Preconditions

- User is logged in to `{{base_url}}` with access to all sections
- A private project and a team project with entities in every section

## Test Data

| Section | Tabs (private / team) | Filters behind the icon | + Add |
|---------|------------------------|-------------------------|-------|
| Agents | Yours / Team + Discover | Folders, Tags | Dropdown: New, Import from file, Build with AI |
| Skills | Yours / Team + Discover | Folders, Tags | Dropdown: New, Import from file, Build with AI |
| Pipelines | None | Folders, Tags | Dropdown: New, Import from file, Build with AI |
| Toolkits & Indexes | None | Folders, Types | Direct button |
| MCPs | None | Folders, Types | Direct button |
| Applications | Yours / Team + Discover | Types (no Folders) | Direct button |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the private project, open the section from the Test Data row via Explore | Title is the section name; tabs match the private-project value; Card view by default |
| 2 | Look at the page without clicking anything | No filters are visible |
| 3 | Click the filter icon, then click it again | The filters from the row appear in a right-side panel, then hide |
| 4 | Enter a search term, switch to Table view and back | The search is kept |
| 5 | Click **+ Add** | It matches the row: a dropdown with three options or a direct button that opens the existing creation flow; close it without saving |
| 6 | Switch to the team project | Tabs match the team-project value (Team instead of Yours) |
| 7 | Repeat for every Test Data row | All rows pass |

## Expected Final State

No entity was created; every section page matches the Test Data.

## Pass/Fail Criteria

**Pass:**
- Tabs, filters and + Add match every row; filters are hidden until the icon is clicked

**Fail:**
- Any section shows wrong tabs, visible filters on load, wrong filter content, or the wrong + Add type

## Notes

**Source functional tests:** ELITEA-5018, ELITEA-5019, ELITEA-5020
**Regression rationale:** Every section page shares the new header; a break blocks finding or creating entities.
**Selected checkpoints:** Tabs by project type; filter panel hidden by default and toggled by the icon; search kept on view switch; + Add type.
