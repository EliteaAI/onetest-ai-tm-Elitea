---
id: ELITEA-1717
title: Verify PGVector credential selection persists when saving agent/toolkit configuration
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:agents, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1717: Verify PGVector credential selection persists when saving agent/toolkit configuration

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that PGVector credential selection persists correctly when saving agent configuration, surviving save/reload cycles without data loss.


## Preconditions

- User is logged in to `{{base_url}}`
- At least 2 PGVector credentials exist
- User is creating or editing an agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Credential | test-pgvector-config |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Page loads |
| 2 | Create a new agent OR open existing agent | Agent configuration page opens |
| 3 | Expand "Toolkit" section | Section expands |
| 4 | Click "Pgvector Configuration" dropdown | Dropdown opens |
| 5 | Select a specific credential (e.g., "test-pgvector-config") | Credential is selected; dropdown closes |
| 6 | Verify selection appears in the field | "test-pgvector-config" displays in PGVector Configuration field |
| 7 | Make other changes to agent config (add description, change model, etc.) | Changes are made |
| 8 | Click "Save" button | Agent saves successfully; success message appears |
| 9 | Close the agent configuration | Agent closes |
| 10 | Reopen the same agent | Agent configuration reopens |
| 11 | Expand "Toolkit" section and check PGVector Configuration field | Selected credential "test-pgvector-config" is still displayed |
| 12 | Open PGVector dropdown | Checkmark appears next to "test-pgvector-config" |

## Expected Final State

PGVector credential selection persists correctly across save/reload cycles.

## Pass/Fail Criteria

**Pass:**
- Selected credential saves with agent configuration
- After reopening agent, same credential is displayed
- Selection persists with other config changes
- No data loss or credential reset
- Checkmark appears next to saved credential

**Fail:**
- Credential selection doesn't save
- Credential resets after reopening
- Selection is lost when other changes are made
- No checkmark appears
- Data loss occurs
