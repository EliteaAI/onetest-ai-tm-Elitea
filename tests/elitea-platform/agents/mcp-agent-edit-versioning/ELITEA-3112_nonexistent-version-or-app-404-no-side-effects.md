---
id: ELITEA-3112
title: "Safe-Patch Call Against a Nonexistent version_id/application_id Returns 404 With No Side Effects"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3112: Safe-Patch Call Against a Nonexistent version_id/application_id Returns 404

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a safe-patch call targeting a `version_id` or `application_id` that does not exist returns a 404-style error with no side effects.

---

## Preconditions

- None beyond internal-MCP tool access.

---

## Test Data

| Field | Value |
|-------|-------|
| `version_id` | a value guaranteed not to correspond to any real version |
| `application_id` | (separately) a value guaranteed not to correspond to any real application |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with a nonexistent `version_id` (valid `application_id`). | 404-style error, no data created. |
| 2 | Call the safe patch tool with a nonexistent `application_id`. | 404-style error, no data created. |

---

## Expected Final State

Nonexistent targets are rejected cleanly with no side effects.

---

## Actual Result — 2026-09-02

**Pass.** Both cases returned a 404-style error with no side effects observed.

---

## Pass/Fail Criteria

**Pass:** 404-style response for both cases, zero side effects.
**Fail:** Wrong status code, or any data is created/changed.
