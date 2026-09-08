---
id: ELITEA-3262
title: "Agent — Version Switching Updates Interface"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3262: Agent — Version Switching Updates Interface

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting a different version from the dropdown correctly updates the interface and loads the selected version's configuration.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least 2 versions having different configurations
- User has permission to view and switch versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with 2+ versions |
| Version A | base (System Prompt: "You are a helpful assistant") |
| Version B | custom-v1 (System Prompt: "You are a specialized code reviewer") |
| Differentiating Field | System prompt text |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page (Version A loaded) | Agent page loads; version selector shows "base" |
| 2 | Note the current system prompt displayed | System prompt reads: "You are a helpful assistant" |
| 3 | Open the version selector dropdown | Dropdown opens showing all versions including custom-v1 |
| 4 | Click on Version B (custom-v1) to select it | Dropdown closes |
| 5 | Verify the version selector now displays "custom-v1" | Version selector shows "custom-v1" |
| 6 | Verify the system prompt field updates to Version B's content | System prompt now reads: "You are a specialized code reviewer" |
| 7 | Verify form fields, attached resources, and configuration reflect Version B | All configuration elements match Version B settings |
| 8 | Switch back to Version A (base) | Version selector shows "base"; system prompt reverts to "You are a helpful assistant" |

## Expected Final State

After switching to custom-v1: version selector displays "custom-v1"; system prompt shows "You are a specialized code reviewer"; all configuration reflects Version B.

## Pass/Fail Criteria

**Pass:** Version selector updates to new version name; interface fully loads the selected version's configuration; all fields and resources reflect the selected version

**Fail:** Version selector does not update; configuration does not change; partial or incorrect data loads; errors occur during switch
