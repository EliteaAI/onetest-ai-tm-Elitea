---
id: ELITEA-5015
title: "Verify Explore list visibility follows existing permissions and Explore hides when empty"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7564]
---
# ELITEA-5015: Verify Explore list visibility follows existing permissions and Explore hides when empty

## Preconditions

- User A has access to all sections
- User B has limited permissions (some sections were hidden for this user in the previous sidebar)
- If available: a user or project setup where no Explore section is visible

## Test Data

| Section | Visibility rule (same as the previous sidebar) |
|---------|-----------------------------------------------|
| MCPs | Shown only when MCPs are enabled for the project |
| Skills | Hidden only in a public project without the publish right |
| Applications | Shown to everyone |
| Agents, Pipelines, Toolkits & Indexes, Credentials | Shown by the existing permission groups |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User A and open the **Explore** list | All sections are listed in the order Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Applications, Credentials |
| 2 | Log in as User B and open the **Explore** list | Only the sections User B could see in the previous sidebar are listed, in the same relative order |
| 3 | As User B, open the URL of a hidden section directly | Access behaves as it did before the change |
| 4 | Select a public project as a user without the publish right and open **Explore** | **Skills** is not listed; the other visible sections are |
| 5 | If a setup with no visible sections is available, look at the sidebar | **Explore** is not shown |

## Expected Final State

Explore shows exactly the sections the user may access.

## Pass/Fail Criteria

**Pass:**
- Each section row follows the same visibility rule as its menu item in the previous sidebar
- Explore is hidden when no section is visible

**Fail:**
- A section is shown to a user who could not see it before, or hidden from a user who could
- Explore is shown with an empty list
