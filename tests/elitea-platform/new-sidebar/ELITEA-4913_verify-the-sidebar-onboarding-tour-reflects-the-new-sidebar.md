---
id: ELITEA-4913
title: "Verify the sidebar onboarding tour reflects the new sidebar"
priority: medium
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7562]
---
# ELITEA-4913: Verify the sidebar onboarding tour reflects the new sidebar


## Preconditions

- User is logged in to `{{base_url}}` as a user who hasn't completed the sidebar tour (or the tour is restarted from Help)

## Test Data

| Group | Steps |
|-------|-------|
| Removed (must NOT appear), 9 steps in `sidebarTour.constants.js` | Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, ELITEA Catalog |
| Replaced | `+ Create Button` step becomes a New chat step ("creates a chat; everything else is + Add in its section") |
| New (must appear) | Explore (hover or click opens the sections, Credentials last); Chat history (folders; wording of Pinned / Recent depends on #7563) |
| Kept (must still work) | ELITEA Logo, Notifications, Project Switcher, Artifacts, Settings, Help Center, Support Assistant |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start the sidebar onboarding tour | The tour starts with its first step |
| 2 | Go through every step | Each step points at an existing, visible sidebar element |
| 3 | Check the steps against the "Removed" column | None of the removed steps appear |
| 4 | Check the steps against the "New" column | All new steps appear with the described text |
| 5 | Check the kept steps (Logo, Notifications, Project Switcher, Artifacts, Settings, Help Center, Support Assistant) | Each still points at its element in the new layout, including the bell and the Support Assistant in the bottom row |
| 6 | Finish the tour | The tour closes with no errors, and the sidebar is in its normal state |

## Expected Final State

The tour describes the new sidebar only.

## Pass/Fail Criteria

**Pass:**
- No step targets a removed item, and all new steps are present and anchored correctly

**Fail:**
- A step points at nothing or at a removed item, a new step is missing, or the tour breaks
