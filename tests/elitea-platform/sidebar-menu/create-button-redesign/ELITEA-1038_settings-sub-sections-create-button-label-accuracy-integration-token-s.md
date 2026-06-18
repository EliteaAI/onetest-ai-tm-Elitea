---
id: ELITEA-1038
title: "Settings Sub-sections: Create Button Label Accuracy (Integration, Token, Secret, Invite User)"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1038: Settings Sub-sections: Create Button Label Accuracy (Integration, Token, Secret, Invite User)

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify the Create button displays the correct context-specific label on each Settings sub-section page.

**Coverage:**
- `+ Integration` on AI Configuration
- `+ Token` on Personal Tokens
- `+ Secret` on Secrets
- `+ Invite User` on Users

## Preconditions

- Logged in to ELITEA with admin or appropriate permissions
- Sidebar in expanded state
- Navigate to Settings

## Test Data

| Settings Sub-section | Expected Label |
|---|---|
| AI Configuration | `+ Integration` |
| Personal Tokens | `+ Token` |
| Secrets | `+ Secret` |
| Users | `+ Invite User` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > AI Configuration | Create button shows `+ Integration` (split button style) |
| 2 | Navigate to Settings > Personal Tokens | Create button updates to `+ Token` |
| 3 | Navigate to Settings > Secrets | Create button updates to `+ Secret` |
| 4 | Navigate to Settings > Users | Create button updates to `+ Invite User` |

## Expected Final State

Create button updates to `+ Invite User`

## Pass/Fail Criteria

**Pass:**
- Each Settings sub-section shows exactly the correct entity-specific label

**Fail:**
- Wrong label shown for any sub-section
- Button shows generic `+ Create` or only `+`
