---
id: ELITEA-0255
title: "View State Isolation Between Request App and Configured Tabs"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770, EliteaAI/elitea_issues#4900]
---
# ELITEA-0255: View State Isolation Between Request App and Configured Tabs

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that the view state (grid vs. list) on the Configured tab does not bleed into the Request App tab.

**Coverage:**
- Switching to list view on Configured tab then going to Request App shows card view
- No action column options visible on Request App tab
- Direct navigation always shows default card view
- Configured tab retains its own view preference independently

## Preconditions

- Logged in as a project member
- On the Applications page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Configured tab | Default grid/card view is shown |
| 2 | Switch the Configured tab to list/table view using the toggle icon | List view with table columns is shown on Configured tab |
| 3 | Click the 'Request App' tab | Request App tab is shown in card view — NOT in table view; no action column options are visible |
| 4 | Navigate away from Applications entirely (e.g., to Agents) and return directly to Applications | Request App tab shows default card view regardless of any previous session state |
| 5 | Navigate to the Configured tab | List view preference from step 2 is retained on the Configured tab |

## Expected Final State

List view preference from step 2 is retained on the Configured tab

## Pass/Fail Criteria

**Pass:**
- Request App always shows card view regardless of Configured tab state
- Configured tab retains its own view state independently

**Fail:**
- Request App shows table view after switching on Configured tab, or action column appears on Request App
