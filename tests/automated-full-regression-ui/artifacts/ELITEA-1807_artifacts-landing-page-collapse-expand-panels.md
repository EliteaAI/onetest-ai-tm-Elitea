---
id: ELITEA-1807
title: "Artifacts Landing Page – Collapse and Expand Panels"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_landing_page_collapse_expand_panels.TestArtifactsLandingPageCollapseExpandPanels.test_collapse_and_expand_panels_independently
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1625
requirements: []
---

# ELITEA-1807: Artifacts Landing Page – Collapse and Expand Panels

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the BUCKETS panel and the main navigation sidebar can each be independently collapsed and expanded, and that their states are independent of each other.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one bucket is present so both panels are visible.

---

## Test Data

| Field | Value |
|-------|-------|
| Sidebar items | Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Agent HUB |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts page with at least one bucket present so both panels are visible | Both panels are visible |
| 2 | Click the << icon at the top-right of the BUCKETS left panel | BUCKETS panel collapses fully and >> icon appears |
| 3 | Click the >> icon | BUCKETS panel is restored to its full expanded state with bucket list visible |
| 4 | Click the < icon on the left edge of the main navigation sidebar | Sidebar collapses to icon-only mode and > icon appears |
| 5 | Click the > icon | Sidebar expands back to full mode showing both icons and labels (Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Agent HUB) |
| 6 | Verify that collapsing/expanding the BUCKETS panel (<</>>) does not affect the sidebar state | Sidebar state remains unchanged when BUCKETS panel is toggled |
| 7 | Verify that collapsing/expanding the sidebar (</>) does not affect the BUCKETS panel state | BUCKETS panel state remains unchanged when sidebar is toggled |

---

## Expected Final State

Both the BUCKETS panel and the navigation sidebar can be independently collapsed and expanded without affecting each other's state. All sidebar labels and bucket list items are visible after each expansion.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each panel collapses and expands correctly and independently.

**Fail:**
- Any step produces an error or unexpected result.
- Collapsing one panel affects the state of the other, or icons/labels are missing after expansion.
