---
id: ELITEA-0965
title: "Admin-Driven Content Update Reflected on Resources Page"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0965: Admin-Driven Content Update Reflected on Resources Page

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify that content changes made by an admin in the ELITEA Admin panel are reflected on the user-facing Resources page.

**Coverage:**
- Admin can add a link to a card
- New link appears on the user-facing Resources page
- Removing a link also removes it from the Resources page
- No unintended side effects on other cards

## Preconditions

Admin account available with access to ELITEA Admin panel (Configuration → Resources)
Standard user account to verify user-facing results

## Test Data

Test link: Title = "Test Link QA", URL = "https://example.com"
Target card: Documentation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA Admin with admin credentials. | ELITEA Admin panel loads. |
| 2 | Navigate to Configuration → Resources. | Resources configuration page loads with all 5 card configuration blocks. |
| 3 | Add a new test link (e.g., title: "Test Link QA", URL: "https://example.com") to the Documentation card. | New link is added to the Documentation card configuration. |
| 4 | Save the changes. | Changes saved without error. |
| 5 | Log in as a standard user and navigate to the Resources page. | Resources page loads. |
| 6 | Locate the Documentation card and confirm the new "Test Link QA" link is visible. | "Test Link QA" link appears in the Documentation card. |
| 7 | Verify no other card content was unintentionally modified. | All other cards display unchanged content. |

## Expected Final State

All other cards display unchanged content.

## Pass/Fail Criteria

**Pass:**
- New link added by admin appears on the Resources page for a standard user
- Removed link no longer appears on the Resources page
- No other card content was unintentionally modified

**Fail:**
- Admin-added link does not appear on the user-facing Resources page
- Removed link still appears after admin deletion
- Unintended changes appear on other cards
