---
id: ELITEA-5018
title: "Verify Agents, Skills and Pipelines section pages: tabs, views, hidden filter panel and Add menu"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7565]
---
# ELITEA-5018: Verify Agents, Skills and Pipelines section pages: tabs, views, hidden filter panel and Add menu

## Preconditions

- User is logged in to `{{base_url}}`
- A private project and a team project, each with agents, skills and pipelines, some of them in folders and with tags
- At least one published agent and one published skill exist

## Test Data

| Section | Private project tabs | Team project tabs | Search placeholder |
|---------|----------------------|-------------------|--------------------|
| Agents | Yours / Discover | Team / Discover | Search agents |
| Skills | Yours / Discover | Team / Discover | Search skills |
| Pipelines | No tabs | No tabs | Search pipelines |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the private project, open **Agents** from Explore | Title **Agents**; tabs as in the Test Data with **Yours** selected; Card view by default; toolbar: view switch → search with filter icon → **+ Add** |
| 2 | Look at the page without clicking anything | **Folders** and **Tags** are not visible |
| 3 | Click the filter icon in the search field | A panel opens on the right with **Folders** (including folder creation) and **Tags** |
| 4 | Select a folder or a tag, then click the filter icon again | The list shows only matching entities; the panel hides and the filter stays applied |
| 5 | Enter a search term, switch to Table view and back | The search and filters are kept |
| 6 | Open **Discover** | Published agents are shown; no filters are visible until the filter icon is clicked, then the catalog filters (e.g. Featured, Categories) appear instead of Folders/Tags |
| 7 | Switch to the team project | The tab label changes to **Team** and the list shows that project's entities |
| 8 | Repeat steps 1–6 for **Skills** and steps 1–5 for **Pipelines** | Same behaviour; Pipelines has no tabs |
| 9 | Click **+ Add** on each page and choose each option | A dropdown with **New**, **Import from file** and **Build with AI**; each opens the existing flow for that entity in the selected project |

## Expected Final State

The user is on a section page, the filter panel is hidden and nothing was created.

## Pass/Fail Criteria

**Pass:**
- Tabs, labels and placeholders match the Test Data
- Folders, Tags and catalog filters are hidden until the filter icon is clicked and toggle with it
- Search and filters survive the view switch; every Add option opens the correct flow

**Fail:**
- Filters are visible on page load or don't toggle with the icon
- Discover shows Folders/Tags, or Pipelines shows tabs
- The tab label ignores the project type, or an Add option opens the wrong flow
