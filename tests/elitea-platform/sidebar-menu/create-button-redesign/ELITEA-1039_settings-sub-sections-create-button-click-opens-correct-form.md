---
id: ELITEA-1039
title: "Settings Sub-sections: Create Button Click Opens Correct Form"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1039: Settings Sub-sections: Create Button Click Opens Correct Form

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the label part of the Create split button on each Settings sub-section opens the correct creation form.

**Coverage:**
- Integration creation from AI Configuration
- Token creation from Personal Tokens
- Secret creation from Secrets
- User invite from Users

## Preconditions

- Logged in to ELITEA with admin/appropriate permissions
- Sidebar in expanded state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > AI Configuration; click `+ Integration` | Integration creation form/flow opens |
| 2 | Navigate to Settings > Personal Tokens; click `+ Token` | Personal Token creation form opens |
| 3 | Navigate to Settings > Secrets; click `+ Secret` | Secret creation form opens |
| 4 | Navigate to Settings > Users; click `+ Invite User` | User invitation form opens |

## Expected Final State

User invitation form opens

## Pass/Fail Criteria

**Pass:**
- Each click opens the correct creation form for that Settings sub-section

**Fail:**
- Wrong form opens
- Nothing happens on click
- Dropdown opens instead of direct navigation
