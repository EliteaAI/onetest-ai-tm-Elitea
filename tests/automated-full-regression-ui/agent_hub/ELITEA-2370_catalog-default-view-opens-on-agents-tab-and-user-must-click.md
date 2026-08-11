---
id: ELITEA-2370
title: "Catalog — default view opens on Agents tab and user must click Skills to navigate to Skills"
priority: high
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_catalog_default_agents_tab.TestCatalogDefaultAgentsTab.test_catalog_default_agents_tab_and_skills_navigation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1437
---

# ELITEA-2370: Catalog — default view opens on Agents tab and user must click Skills to navigate to Skills

**Module:** agent-hub · **Priority:** high · **Type:** functional

**Objective:** Verify that Catalog — default view opens on Agents tab and user must click Skills to navigate to Skills. Success is confirmed when verify the right panel shows featured (trending, my liked) and categories filters.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click "Catalog" in the left sidebar navigation | Control responds; expected next state is shown. |
| 2 | Verify the "Welcome to ELITEA Catalog!" page loads | Condition holds as described. |
| 3 | Verify the Agents tab is selected by default (underlined/highlighted) | Condition holds as described. |
| 4 | Verify the Skills tab is visible next to Agents tab with a lightning bolt icon | Condition holds as described. |
| 5 | Verify the main content area displays Agents content by default | Condition holds as described. |
| 6 | Click the "Skills" tab | Control responds; expected next state is shown. |
| 7 | Verify the Skills tab becomes active/highlighted | Condition holds as described. |
| 8 | Verify the main content area switches to display Skills content with Trending and category sections | Condition holds as described. |
| 9 | Verify the right panel shows FEATURED (Trending, My Liked) and CATEGORIES filters | Condition holds as described. |

---

## Expected Final State

Verify the right panel shows FEATURED (Trending, My Liked) and CATEGORIES filters.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — default view opens on Agents tab and user must click Skills to navigate to Skills.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
