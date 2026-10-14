---
id: ELITEA-3740
title: "Budget Warnings — Member vs Project Scope Selection, Texts, Links and Independent Dismissal"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3740: Budget Warnings — Member vs Project Scope Selection, Texts, Links and Independent Dismissal

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that only one banner is shown when both the member and the project budget are near their limits, that the higher level wins (member wins ties), and that each scope has its own text, link and dismissal.

**Coverage:**
- Member-only and project-only banner text and links
- Higher level wins; member wins ties
- Separate dismissal key per scope

## Preconditions

- Logged in to `{{base_url}}`; Cost Budgets mode = **enforce**; dismissal switch **ON**
- Admin can set both a member limit and a project limit on the test team project

## Test Data

| Scope | Banner text | Link | Link target |
|-------|-------------|------|-------------|
| member | "You have used N% of your budget in this project." | View my usage | `/settings/usage?scope=user` |
| project | "You have used N% of your budget." | View usage | `/settings/usage` |

| Member % | Project % | Expected banner |
|----------|-----------|-----------------|
| 85 | 96 | project (95 beats 80) |
| 85 | 86 | member (tie at 80, member wins) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set only a member limit; push member spend to ~91% | Member banner at level 90, with member text and a "View my usage" link to `/settings/usage?scope=user` |
| 2 | Remove the member limit and set only a project limit; push project spend over the threshold | Project banner with project text and a "View usage" link to `/settings/usage` |
| 3 | Set both limits to reach each row of the scope-priority table | Banner scope matches the table, and so does the API `scope` field |
| 4 | At member 85% / project 86%, dismiss the member banner, then push project spend to ≥ 90% | Project banner **shows** (higher level, separate key) |
| 5 | Dismiss the project banner | A separate `…project.{YYYY-MM}` localStorage key is written; the member key is unchanged |

## Expected Final State

Both scope dismissal keys exist independently in localStorage.

## Pass/Fail Criteria

**Pass:**
- Correct text and link per scope
- Scope selection follows the priority table
- Each scope is dismissed independently

**Fail:**
- Two banners at once, or the wrong scope chosen
- Dismissing one scope hides the other scope's higher-level banner
