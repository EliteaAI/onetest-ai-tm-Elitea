---
id: ELITEA-4898
title: "Verify Explore opens on hover and lists sections in the specified order"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4898: Verify Explore opens on hover and lists sections in the specified order


## Preconditions

- User is logged in to `{{base_url}}` as a user with access to all sections
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Expected order | Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Applications, Credentials |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Hover the pointer over **Explore** | The section list opens next to the sidebar |
| 2 | Read the items in the list | The items appear in this order: Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Applications, Credentials (last) |
| 3 | Move the pointer from **Explore** onto the list | The list stays open |
| 4 | Move the pointer away from both Explore and the list | The list closes (after a short delay of about 200 ms) |

## Expected Final State

The Explore list is closed and the current page is unchanged.

## Pass/Fail Criteria

**Pass:**
- Hovering opens the list, and the order matches the Test Data
- The list stays open on the move to it and closes when the pointer leaves both

**Fail:**
- The list doesn't open on hover, closes while moving onto it, or stays open after leaving
- The sections are missing or out of order
