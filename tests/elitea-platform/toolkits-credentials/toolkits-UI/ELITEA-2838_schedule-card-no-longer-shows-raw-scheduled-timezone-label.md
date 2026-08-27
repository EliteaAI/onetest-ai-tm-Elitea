---
id: ELITEA-2838
title: "Schedule Card No Longer Shows Raw 'Scheduled: <timezone>' Label"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6296]
---
# ELITEA-2838: Schedule Card No Longer Shows Raw 'Scheduled: <timezone>' Label

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the schedule card no longer displays the raw creator-timezone label (e.g. "Scheduled: Europe/Minsk, Shown: Asia/Yerevan") alongside an un-converted time — per the fix agreed in the issue thread, the card should show only the already-converted time in the viewer's own timezone, with no ambiguous dual-timezone wording.

**Coverage:**
- "Scheduled: <tz-name>" / "Shown: <tz-name>" style labeling is removed from the schedule card
- The displayed time is the converted value only (viewer's local time), not paired with a raw offset/zone-name string that could be misread as the time-to-use
- If a timezone indicator is kept, it unambiguously reflects the viewer's own timezone (not the creator's)

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with an index that has an existing configured schedule (created by a different user/timezone if possible)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexing |
| Index | An index with a configured schedule created under a different timezone than the current viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Index Details page for an index with a configured schedule. | Index details page displays. |
| 2 | Expand the SCHEDULE section and observe the schedule card text. | Card shows the scheduled time only — no "Scheduled: <tz-name>, Shown: <tz-name>" style wording. |
| 3 | Check whether any timezone context is still displayed next to the time. | If present, it clearly refers to the viewer's own local timezone only — not a second, creator-side timezone label. |
| 4 | Compare against the "Next run" field on the same card. | "Next run" and the scheduled time use the same (viewer's) timezone consistently — no mismatch between the two fields as previously reported. |

## Expected Final State

Schedule card shows a single, unambiguous time already converted to the viewer's local timezone, with no leftover raw creator-timezone label.

## Pass/Fail Criteria

**Pass:**
- No "Scheduled: <tz>, Shown: <tz>" style dual-timezone wording remains
- Displayed time and "Next run" are both consistently in the viewer's own timezone

**Fail:**
- The old raw timezone-offset label (e.g. "Scheduled: Europe/Minsk") is still shown next to an un-converted time
- Scheduled time and "Next run" use inconsistent timezones on the same card
