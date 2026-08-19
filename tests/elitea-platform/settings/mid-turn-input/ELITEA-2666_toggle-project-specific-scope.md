---
id: ELITEA-2666
title: "Verify Mid-turn Input toggle is project-specific"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to at least two projects

## Test Data

| Field | Value |
|-------|-------|
| Project A | Private project |
| Project B | Team project |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch to Project A | Project A is selected |
| 2 | Navigate to Settings and enable Mid-turn Input toggle | Toggle is ON |
| 3 | Switch to Project B | Project B is selected |
| 4 | Navigate to Settings and check Mid-turn Input toggle | Toggle state is independent (may be OFF) |
| 5 | Leave toggle OFF in Project B | Toggle remains OFF |
| 6 | Switch back to Project A | Project A selected |
| 7 | Verify toggle is still ON | Toggle remains ON in Project A |

## Expected Final State

Toggle state is project-specific; changes in one project do not affect other projects.

## Pass/Fail Criteria

**Pass:**
- Toggle state is independent per project
- Changing one project doesn't affect others

**Fail:**
- Toggle state is global across projects
- Changes propagate to other projects
