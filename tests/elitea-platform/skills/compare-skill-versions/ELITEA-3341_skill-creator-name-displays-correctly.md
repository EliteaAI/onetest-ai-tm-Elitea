---
id: ELITEA-3341
title: "Creator name displays correctly for Skill versions instead of 'BY AUTHOR UNAVAILABLE'"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6, bug:6563]
requirements: [EliteaAI/elitea_issues#6304, EliteaAI/elitea_issues#6563]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skill exists with 2+ versions created by different users

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version 1 Creator | Current user (e.g., "Alice Smith") |
| Version 2 Creator | Different user in same org (e.g., "Bob Jones") |
| Version 3 Creator | System-created (if applicable) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill Version 1 as current user | Version created successfully |
| 2 | Share Skill with another user in same org or have them create Version 2 | Version 2 created by different user |
| 3 | Open Compare Versions modal comparing Version 1 and Version 2 | Modal opens successfully |
| 4 | Verify Version 1 column header or metadata displays the actual creator name (e.g., "Alice Smith") | Creator name "Alice Smith" is visible |
| 5 | Verify NO version shows "BY AUTHOR UNAVAILABLE" | Creator metadata is properly fetched and displayed |
| 6 | Verify Version 2 column displays the actual creator name (e.g., "Bob Jones") | Creator name "Bob Jones" is visible |
| 7 | Close modal and select a system-created version (if applicable) | Version selected |
| 8 | Open Compare Versions modal with system-created version | Modal opens |
| 9 | Verify system-created version displays appropriate creator label (e.g., "System" or "Auto-generated") | Creator label is displayed (not "BY AUTHOR UNAVAILABLE") |
| 10 | Test with multiple version combinations: current user vs different user, current user vs system, different user vs system | All combinations display correct creator names |

## Expected Final State

Creator metadata is properly fetched and displayed for all Skill versions. NO version displays "BY AUTHOR UNAVAILABLE".

## Pass/Fail Criteria

**Pass:**
- Each version displays the actual creator name or appropriate label
- No version shows "BY AUTHOR UNAVAILABLE"
- Creator names are correct for versions created by current user, different users, and system

**Fail:**
- Any version shows "BY AUTHOR UNAVAILABLE"
- Creator names are missing or incorrect
- Creator metadata not displayed
