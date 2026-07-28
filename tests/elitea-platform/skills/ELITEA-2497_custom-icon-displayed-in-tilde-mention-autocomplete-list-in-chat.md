---
id: ELITEA-2497
title: "Custom icon displayed in tilde mention autocomplete list in chat"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An Agent with at least one Skill with custom icon attached exists
- An Agent with at least one Skill without custom icon attached exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Agent | Agent with mixed Skills (some with custom icons, some without) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a new conversation with the Agent that has Skills attached | Chat conversation opens |
| 2 | In the chat composer, type `~` | Mention autocomplete dropdown appears |
| 3 | Verify the dropdown lists attached Skills | Skills are listed |
| 4 | Locate the Skill with a custom icon | Skill is visible in dropdown |
| 5 | Verify the Skill displays its custom icon in the dropdown | Custom icon shown next to Skill name |
| 6 | Locate a Skill without custom icon | Skill is visible in dropdown |
| 7 | Verify the Skill displays the default `skill-icon.svg` | Default icon shown |

## Expected Final State

The `~mention` autocomplete dropdown in chat displays custom icons for Skills that have them and default icons for Skills without.

## Pass/Fail Criteria

**Pass:**
- Custom icon displays for Skill with custom icon
- Default icon displays for Skill without custom icon
- All attached Skills appear in dropdown

**Fail:**
- Icons not displayed in dropdown
- Wrong icons displayed
- Dropdown fails to appear
