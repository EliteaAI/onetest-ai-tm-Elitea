---
id: ELITEA-4926
title: "Explore opens by hover, click and keyboard and navigates to sections"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4926: Explore opens by hover, click and keyboard and navigates to sections

## Preconditions

- User is logged in to `{{base_url}}` as a user with access to all sections
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Expected order | Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Applications, Credentials |
| Same-tab section | Agents |
| New-tab sections | Pipelines (Ctrl/Cmd-click), Credentials (middle-click) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Hover the pointer over **Explore** | The section list opens next to the sidebar |
| 2 | Read the items in the list | They appear in the expected order, with Credentials last |
| 3 | Move the pointer from Explore onto the list, then away from both | The list stays open while moving onto it and closes after the pointer leaves both |
| 4 | Click **Explore**, then click outside the list | The list opens on click and closes on the outside click |
| 5 | Tab to **Explore**, press Enter, move to **Agents** with the keyboard and press Enter | The Agents page opens and the list closes |
| 6 | Check the sidebar, then hover Explore | Explore is shown as selected, and Agents is highlighted in the list |
| 7 | Ctrl/Cmd-click **Pipelines** in the list | Pipelines opens in a new tab, and the current tab stays on Agents |
| 8 | Middle-click **Credentials** in the list | Credentials opens in a new tab, and the current tab stays on Agents |
| 9 | Click **Artifacts** | Artifacts is selected and Explore is no longer selected |

## Expected Final State

Explore works with every input method, its rows are real links, and the selection state follows the open page.

## Pass/Fail Criteria

**Pass:**
- The list opens by hover, click and keyboard, in the expected order
- Rows open sections in the same tab and in new tabs
- Explore and the active section are highlighted on a section page only

**Fail:**
- Explore doesn't open by any one input method, or the sections are missing or out of order
- A modified click navigates the current tab instead of opening a new one
- Highlighting is missing, wrong, or stays on non-section pages

## Notes

**Source functional tests:** ELITEA-4898, ELITEA-4899, ELITEA-4905, ELITEA-4907
**Regression rationale:** Explore replaces every entity menu item, so a break here blocks access to all sections.
**Selected checkpoints:** Hover open/close; click; keyboard; order; same-tab and new-tab navigation; Explore and section highlight.
