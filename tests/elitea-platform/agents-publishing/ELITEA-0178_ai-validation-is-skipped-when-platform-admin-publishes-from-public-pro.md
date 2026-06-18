---
id: ELITEA-0178
title: "AI Validation Is Skipped When Platform Admin Publishes From Public Project Admin Section"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3773, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3773]
---
# ELITEA-0178: AI Validation Is Skipped When Platform Admin Publishes From Public Project Admin Section

**Module:** Agents Publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a platform admin uploads and publishes an agent from the Public Project Admin section using an agent config that has deliberately incomplete/poor-quality metadata (which would fail AI quality validation for regular users), no AI validation dialog, critical error, or warning is shown — the publish proceeds directly.

**Coverage:**
- Admin upload flow does not invoke AI quality validation checks
- Agent with no description, generic name, no icon, no conversation starters is published without validation errors or warnings
- Admin publish is immediate ("direct publish" path, no quality gate)
- Regular user publishing the same incomplete config via normal flow would be blocked by AI validation (confirming the bypass is admin-specific)

## Preconditions

- Logged in as Platform Admin on {{base_url}}
- Incomplete agent config file prepared: name = "New Agent", no description, default icon, no tags, no conversation starters, minimal instructions (10-word instruction only)
- Regular user account (User A) available for baseline comparison

## Test Data

- Incomplete agent config attributes:
  - Name: "New Agent"
  - Description: (empty)
  - Icon: (platform default)
  - Tags: (none)
  - Conversation starters: (none)
  - Instructions: 10-word minimal instruction only

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As Platform Admin, navigate to Public Project → Agents → Admin section | Admin section loads |
| 2 | Click Upload/Publish | Upload dialog opens |
| 3 | Upload the incomplete agent config (name "New Agent", no description, default icon, no tags, no starters) | File accepted by dialog |
| 4 | Confirm the upload/publish | Publish completes without any AI validation dialog, quality check screen, or critical/warning messages about missing description or generic name |
| 5 | Navigate to Agents Studio | "New Agent" (or the name from the config) appears in Studio |
| 6 | (Baseline comparison) As User A, navigate to their own agent, click "Publish" | Normal publish modal opens |
| 7 | As User A, enter a version name, check agreement, click Publish on an agent with the same incomplete metadata | AI validation dialog appears showing critical errors or warnings about missing description, generic name, etc. — blocking or warning the regular user |

## Expected Final State

AI validation dialog appears showing critical errors or warnings about missing description, generic name, etc. — blocking or warning the regular user

## Pass/Fail Criteria

**Pass:**
- Admin publish completes without any AI validation dialog or quality gate
- Incomplete metadata agent is published directly to Agents Studio via admin path
- Regular user attempting publish of same incomplete metadata sees AI validation (confirming admin bypass is intentional and working)

**Fail:**
- AI validation dialog appears during admin upload flow (same as regular user)
- Admin publish is blocked due to missing description, generic name, or other quality checks
- Incomplete agent is not published despite admin attempting it
- Regular user also bypasses AI validation (validation is broken, not admin-specific)
