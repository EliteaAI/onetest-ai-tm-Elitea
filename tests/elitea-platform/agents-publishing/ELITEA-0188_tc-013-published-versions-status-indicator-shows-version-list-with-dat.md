---
id: ELITEA-0188
title: "TC-013: Published Versions Status Indicator Shows Version List With Dates and Per-Version Unpublish"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0188: TC-013: Published Versions Status Indicator Shows Version List With Dates and Per-Version Unpublish

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that an agent with published versions shows a "Published" status indicator, lists all published versions with names and dates, and allows individual version unpublishing.

Coverage:
- "Published" badge/indicator visible on agent with published versions
- All published versions listed with name + publication date
- Per-version unpublish option available
- Unpublishing one version does not affect other published versions

## Preconditions

- Logged in as User A
- Agent A has two published versions: 'v1.0' and 'v2.0'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A from the Agents project list | Agent A detail page loads |
| 2 | Look for a 'Published' status badge or indicator | A 'Published' badge/label is visible on the agent card or header |
| 3 | Locate the published versions list | A list showing both v1.0 and v2.0 is visible |
| 4 | Verify version details for each entry | Each version shows: version name, publication date/timestamp |
| 5 | Verify each version has its own Unpublish option | Both v1.0 and v2.0 have individual Unpublish actions |
| 6 | Unpublish v1.0 | v1.0 is removed from the list; v2.0 remains listed with status 'Published' |

## Expected Final State

v1.0 is removed from the list; v2.0 remains listed with status 'Published'

## Pass/Fail Criteria

PASS:
- "Published" status indicator visible when versions are published
- Both versions listed with names and publication dates
- Each version has an individual Unpublish option
- Unpublishing v1.0 leaves v2.0 unaffected and still listed

FAIL:
- No "Published" indicator visible despite published versions existing
- Published versions not listed or missing publication dates
- Unpublishing one version also removes or affects the other
