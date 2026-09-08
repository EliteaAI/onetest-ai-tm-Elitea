---
id: ELITEA-3326
title: "Tools and Skills section displays dependency lists as read-only in Agent comparison"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions having different Tools and Skills attached

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 Tools | GitHub Toolkit, JIRA Toolkit |
| Version 1 Skills | Data Analysis Skill |
| Version 2 Tools | GitHub Toolkit, Slack Toolkit |
| Version 2 Skills | Data Analysis Skill, Report Generator Skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Navigate to Tools & Skills section | Section loads |
| 3 | Verify "Tools" subsection is displayed for both versions | Tools list visible in both columns |
| 4 | Verify Version 1 Tools list shows: GitHub Toolkit, JIRA Toolkit | Correct tools listed for Version 1 |
| 5 | Verify Version 2 Tools list shows: GitHub Toolkit, Slack Toolkit | Correct tools listed for Version 2 |
| 6 | Verify differences are highlighted: JIRA in v1 only, Slack in v2 only | Diff highlighting shows JIRA and Slack as differences |
| 7 | Verify "Skills" subsection is displayed for both versions | Skills list visible in both columns |
| 8 | Verify Version 1 Skills list shows: Data Analysis Skill | Correct skill listed for Version 1 |
| 9 | Verify Version 2 Skills list shows: Data Analysis Skill, Report Generator Skill | Correct skills listed for Version 2 |
| 10 | Verify differences are highlighted: Report Generator in v2 only | Diff highlighting shows Report Generator as added in v2 |
| 11 | Verify NO "Add Tool" or "Add Skill" buttons are present | No add controls visible |
| 12 | Verify NO "Remove" or "Configure" buttons are present for listed items | No edit controls visible |
| 13 | Attempt to click on a Tool name | No edit action occurs, item is not clickable for editing |
| 14 | Attempt to click on a Skill name | No edit action occurs, item is not clickable for editing |
| 15 | Verify toolkit configurations (if visible) are displayed as read-only text | Configuration details shown as text, not editable fields |

## Expected Final State

Tools & Skills section displays dependency lists for both versions as read-only with diff highlighting for differences. No add/remove/configure controls are available.

## Pass/Fail Criteria

**Pass:**
- Tools and Skills lists displayed for both versions
- List content matches the actual attachments from each version
- Differences are highlighted correctly
- No edit controls present (add/remove/configure buttons)
- Items are not clickable for editing

**Fail:**
- Tools or Skills lists missing
- Incorrect items displayed
- No diff highlighting for differences
- Edit controls are present
- Items can be edited or removed
