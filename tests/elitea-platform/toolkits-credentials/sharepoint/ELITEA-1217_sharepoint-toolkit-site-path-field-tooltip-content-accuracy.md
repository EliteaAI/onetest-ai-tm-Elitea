---
id: ELITEA-1217
title: "SharePoint Toolkit — Site Path Field Tooltip Content Accuracy"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1217: SharePoint Toolkit — Site Path Field Tooltip Content Accuracy

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Site Path field tooltip in the SharePoint toolkit form accurately states the field's purpose, accepted formats, and default behavior. Covers: exact tooltip text match in Create and Edit modes; tooltip readability in dark and light themes.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An existing SharePoint toolkit available for Edit mode test

## Test Data

Expected tooltip text: "SharePoint site path relative to the tenant URL. Use when the credential site_url is only the tenant URL. Examples: sites/site-name or teams/team-name. Leave empty for credentials where site_url already includes the site path."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → + Create → SharePoint. Locate the Site Path field. Hover over the ⓘ icon next to the label. | Tooltip appears. Text reads: 'SharePoint site path relative to the tenant URL. Use when the credential site_url is only the tenant URL. Examples: sites/site-name or teams/team-name. Leave empty for credentials where site_url already includes the site path.' |
| 2 | Open an existing SharePoint toolkit in Edit mode. Hover over the ⓘ icon next to Site Path. | Same tooltip text is present in Edit mode. |
| 3 | Switch to Light theme. Hover over the ⓘ icon. | Tooltip is visible, text is fully readable, not clipped or overflowed. |
| 4 | Switch back to Dark theme. Hover over the ⓘ icon. | Tooltip is visible and readable in dark theme. |

## Expected Final State

Tooltip is visible and readable in dark theme.

## Pass/Fail Criteria

Pass:
- Tooltip text exactly matches the expected string in both Create and Edit modes
- Tooltip is readable in both themes without clipping or overflow

Fail:
- Tooltip text is absent, truncated, or differs from the expected wording
- Tooltip is unreadable (invisible text, overflow, z-index issue) in either theme
