---
id: ELITEA-2839
title: "Schedule Time and Next Run Stay Consistently in Viewer's Timezone Across Edit and Team/Shadow Views"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6296]
---
# ELITEA-2839: Schedule Time and Next Run Stay Consistently in Viewer's Timezone Across Edit and Team/Shadow Views

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the scheduled time is shown correctly converted to the viewer's timezone consistently across every place it appears — the schedule card, the edit/settings modal, and team/shadow-shared views — not just on the primary Index Details card.

**Coverage:**
- Edit/settings modal for the schedule pre-fills with the viewer's own local time equivalent, not the creator's raw time
- Team members / shadow-project viewers see the same correctly-converted time as any other viewer, not the creator's raw time
- Editing and re-saving the schedule as a different-timezone viewer does not corrupt the underlying scheduled instant (still resolves to the same absolute time for all viewers afterward)

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An index with a schedule configured by a user in a different timezone than the current tester
- Access to a team/shared or shadow project view of the same index, if available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexing |
| Index | An index with a schedule created under a different creator timezone |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the current viewer, open the schedule card on Index Details. | Time shown is converted to viewer's own timezone (per ELITEA-2837). |
| 2 | Click the edit (pencil) icon to open the schedule edit/settings modal. | Modal opens showing a time field. |
| 3 | Compare the time pre-filled in the edit modal to the time shown on the card. | Both match — modal does not show the creator's raw time while the card shows the converted time (or vice versa). |
| 4 | Without changing the time, save the modal. | Schedule is unchanged; next run remains correct for all viewers. |
| 5 | Open the same index from a team/shared or shadow-project view (different viewer context, if available). | Scheduled time and next run shown there are also converted to that viewing context's timezone, matching the same underlying instant. |

## Expected Final State

The scheduled time and next run are consistently derived from a single underlying absolute instant and correctly converted everywhere they are surfaced — schedule card, edit modal, and team/shadow views.

## Pass/Fail Criteria

**Pass:**
- Edit modal, schedule card, and team/shadow view all show the time converted to the current viewer's own timezone
- No location shows the creator's raw, un-converted time

**Fail:**
- Edit modal shows a different (e.g. creator's raw) time than the schedule card for the same viewer
- Team/shadow view shows an un-converted or inconsistent time compared to the primary Index Details view
