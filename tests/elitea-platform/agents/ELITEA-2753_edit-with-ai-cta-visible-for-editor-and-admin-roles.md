---
id: ELITEA-2753
title: "Edit with AI CTA is visible and accessible on existing Agent page for users with edit permission"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in to `{{base_url}}` with **Editor** or **Admin** role in a project
- At least one existing, saved Agent is available with Name, Description, Instructions, Welcome Message, Chat Starters configured and at least one Toolkit and one Skill attached

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Editor or Admin |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with Editor or Admin role | Login succeeds and the platform home page loads |
| 2 | Navigate to the Agents menu | The Agents list is displayed |
| 3 | Open an existing Agent's configuration page | The Agent configuration page loads with its saved fields |
| 4 | Locate the "Edit with AI" CTA on the page | The CTA is visible in the General section header, displaying a magic-wand icon and the "Edit with AI" label |
| 5 | Click the "Edit with AI" CTA | The Edit with AI modal opens, showing the prompt entry step |

## Expected Final State

The Edit with AI modal is open and ready for prompt entry; the underlying Agent configuration remains unchanged.

## Pass/Fail Criteria

**Pass:**
- The "Edit with AI" CTA is visible with correct icon and label for Editor/Admin roles
- Clicking the CTA opens the Edit with AI modal

**Fail:**
- The CTA is missing, mislabeled, or unresponsive for a user with edit permission
- Clicking the CTA does not open the modal or throws an error
