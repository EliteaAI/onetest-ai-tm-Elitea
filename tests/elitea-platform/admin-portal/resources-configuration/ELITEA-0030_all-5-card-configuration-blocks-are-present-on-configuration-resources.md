---
id: ELITEA-0030
title: "All 5 Card Configuration Blocks Are Present on Configuration → Resources Page"
priority: critical
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0030: All 5 Card Configuration Blocks Are Present on Configuration → Resources Page

**Module:** Resources Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Configuration → Resources page loads all five expected card configuration blocks: Information, Documentation, Release Notes, Video Library, and Tutorials. Covers AC2 of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Admin → Configuration → Resources. | The Resources configuration page loads without error. |
| 2 | Check the page for an Information card block. | Information block is visible. |
| 3 | Check the page for a Documentation card block. | Documentation block is visible. |
| 4 | Check the page for a Release Notes card block. | Release Notes block is visible. |
| 5 | Check the page for a Video Library card block. | Video Library block is visible. |
| 6 | Check the page for a Tutorials card block. | Tutorials block is visible. |

## Expected Final State

Tutorials block is visible.

## Pass/Fail Criteria

Pass: All five blocks (Information, Documentation, Release Notes, Video Library, Tutorials) are present.
Fail: Any block is missing.
