---
id: ELITEA-4915
title: "Verify no console errors during sidebar interactions"
priority: medium
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4915: Verify no console errors during sidebar interactions


## Preconditions

- User is logged in to `{{base_url}}`
- DevTools Console is open with "Preserve log" enabled and errors filtered

## Test Data

| # | Interaction |
|---|-------------|
| 1 | Hover and click Explore, and open each section |
| 2 | Collapse and expand the sidebar 5 times |
| 3 | Switch project twice |
| 4 | Scroll the chat history to the end (lazy loading) |
| 5 | Open Settings, Help, Support Assistant and the bell |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Clear the console | The console is empty |
| 2 | Perform the interaction from the Test Data row | The interaction completes |
| 3 | Check the console and the Network tab | No new JS errors, React warnings about keys or state, or failed (4xx/5xx) requests caused by the sidebar |
| 4 | Repeat for every row | All rows pass |

## Expected Final State

Sidebar interactions run clean.

## Pass/Fail Criteria

**Pass:**
- No console errors or failed requests caused by any listed interaction

**Fail:**
- Any error, unhandled promise rejection or failed request appears
