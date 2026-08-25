---
id: ELITEA-2754
title: "Edit with AI CTA is not visible for users without edit permission"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User account with **Viewer** role in the project
- At least one existing Agent is available in the same project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with Viewer role | Login succeeds |
| 2 | Navigate to the Agents menu | The Agents list is displayed (read-only affordances only) |
| 3 | Open an existing Agent's configuration page | The Agent configuration page loads in read-only mode |
| 4 | Inspect the General section header where the CTA would appear for editors | The "Edit with AI" CTA is NOT displayed anywhere on the page |
| 5 | Attempt to access the Edit with AI modal via direct URL/route manipulation, if applicable | Access is denied or the modal does not open; no AI edit action is possible |

## Expected Final State

The Agent configuration page renders normally for the Viewer without any Edit with AI entry point.

## Pass/Fail Criteria

**Pass:**
- The "Edit with AI" CTA is absent for the Viewer role in all attempted access paths

**Fail:**
- The CTA is visible, present in the DOM but merely hidden via CSS (still clickable), or the modal can be opened by a Viewer through any route
