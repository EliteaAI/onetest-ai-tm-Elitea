---
id: ELITEA-3211
title: "Share Toggle Tooltip Clearly Explains Cross-Project Readability"
priority: low
type: ui
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui, copy]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3211: Share Toggle Tooltip Copy Clarity

**Module:** Secrets · **Priority:** Low · **Type:** UI

**Objective:** Confirm the share toggle's tooltip/help text clearly communicates what "shared" actually means for a personal secret (readable by other projects/pipelines the owner has access to) so a user isn't left guessing at the consequence of toggling it on.

**Coverage:** TC-UI (tooltip copy clarity)

## Preconditions

- A personal-project secret exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Hover/focus the share toggle for a personal secret. | A tooltip or adjacent help text appears. |
| 2 | Read the tooltip copy. | Copy clearly states the effect of enabling sharing (e.g. "accessible to pipelines/code nodes run under your identity across projects") without ambiguous or misleading wording. |
| 3 | Compare wording for the ON state vs. OFF state (if the tooltip differs by state). | Both states are equally clear about current effect. |

## Expected Final State

A user reading the tooltip understands the real consequence of the toggle before changing it.

## Pass/Fail Criteria

**Pass:**
- Tooltip/help text is present and unambiguous about what sharing does

**Fail:**
- No tooltip/help text at all, or wording is vague/misleading about the actual effect
