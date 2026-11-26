---
id: ELITEA-4907
title: "Verify Explore and the active section are highlighted on a section page"
priority: high
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4907: Verify Explore and the active section are highlighted on a section page


## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| Sections | Agents; Toolkits & Indexes; Credentials |
| Sidebar state | Expanded; Collapsed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Explore → Agents** | The Agents page opens |
| 2 | Check the sidebar | **Explore** is shown as selected |
| 3 | Hover **Explore** | **Agents** is highlighted in the list |
| 4 | Repeat for the other sections and in the collapsed rail | Explore and the matching section are highlighted every time |
| 5 | Open **Artifacts** | Explore is no longer selected and Artifacts is selected |

## Expected Final State

The selection state reflects the open page.

## Pass/Fail Criteria

**Pass:**
- Explore and the current section are highlighted on every section page in both states

**Fail:**
- No highlight, the wrong section is highlighted, or Explore stays selected on non-section pages
