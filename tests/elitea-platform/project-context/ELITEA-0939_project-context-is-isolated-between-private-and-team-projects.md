---
id: ELITEA-0939
title: "Project Context Is Isolated Between Private and Team Projects"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, team-project, story:3395, isolation, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0939: Project Context Is Isolated Between Private and Team Projects

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that Project Context is fully isolated between Private and Team projects — no content or toggle state leaks across projects.

**Coverage:**
- Private project context not visible in Team project and vice versa
- Toggle state is independent per project

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Private project phrase: `PRIVATE-MARKER: Oak tree by the river`
- Team project phrase: `TEAM-MARKER: Pine tree on the hill`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In the Private project, set context to 'PRIVATE-MARKER: Oak tree by the river'. Toggle = ON. Save. | Saved in Private project. |
| 2 | In the Team project, set context to 'TEAM-MARKER: Pine tree on the hill'. Toggle = ON. Save. | Saved in Team project. |
| 3 | Run an agent in the Private project. Ask: 'What is the PRIVATE-MARKER?' then 'What is the TEAM-MARKER?' | Returns 'Oak tree by the river'. Does NOT return the Team marker. |
| 4 | Run an agent in the Team project. Ask: 'What is the TEAM-MARKER?' then 'What is the PRIVATE-MARKER?' | Returns 'Pine tree on the hill'. Does NOT return the Private marker. |
| 5 | Disable toggle in the Private project. Check the Team project toggle. | Team project toggle is unaffected — still ON. |

## Expected Final State

Team project toggle is unaffected — still ON.

## Pass/Fail Criteria

**Pass:**
- Each project's agent only knows its own marker
- Toggle changes in one project do not affect the other

**Fail:**
- Agent in Private project returns Team project marker (or vice versa)
- Enabling toggle in one project enables it in another
