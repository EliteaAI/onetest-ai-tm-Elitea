---
id: ELITEA-0032
title: "Resources Section Appears in Admin Configuration Before Banner"
priority: critical
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0032: Resources Section Appears in Admin Configuration Before Banner

**Module:** Resources Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the new Resources subsection is visible in ELITEA Admin → Configuration and is positioned before the Banner section, as specified in AC1 of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Admin → Configuration. | The Configuration page opens. |
| 2 | Inspect the section list on the Configuration page. | A subsection named Resources is present. |
| 3 | Verify the position of Resources relative to Banner. | Resources appears before Banner in the section list. |

## Expected Final State

Resources appears before Banner in the section list.

## Pass/Fail Criteria

Pass: Resources section is visible and positioned before Banner.
Fail: Resources section is missing or appears after Banner.
