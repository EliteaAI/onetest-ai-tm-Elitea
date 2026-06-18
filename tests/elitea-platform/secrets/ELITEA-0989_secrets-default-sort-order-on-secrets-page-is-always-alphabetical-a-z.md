---
id: ELITEA-0989
title: "[Secrets] Default Sort Order on Secrets Page Is Always Alphabetical A→Z"
priority: medium
type: functional
module: secrets
status: ready
execution_type: manual
tags: [feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4866]
---
# ELITEA-0989: [Secrets] Default Sort Order on Secrets Page Is Always Alphabetical A→Z

**Module:** Secrets · **Priority:** Medium · **Type:** Functional

**Objective:** Regression check — verify the Secrets list consistently opens with A→Z sort order on every visit, regardless of previous navigation history.

**Coverage:**
- Sort order consistency across multiple visits to the Secrets page
- No stale creation-date sort persisting from a previous session
- Baseline default state verification

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Multiple secrets exist with known names spanning different letters (e.g., Alpha, Bravo, Charlie, Delta, Echo)
- Browser: Chrome latest

## Test Data

- Existing secrets (example): Alpha, Bravo, Charlie, Delta, Echo

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Secrets. | Secrets list loads. Items are sorted A→Z alphabetically. |
| 2 | Navigate away to another page (e.g., Agents), then return to Settings → Secrets. | Secrets list loads again sorted A→Z. |
| 3 | Navigate away once more and return to Secrets a second time. | Secrets list loads A→Z — consistent on every visit. |

## Expected Final State

Secrets list loads A→Z — consistent on every visit.

## Pass/Fail Criteria

**Pass:**
- Secrets list opens A→Z on every visit consistently

**Fail:**
- Sort order differs between visits
- List opens in creation-date order on any visit
