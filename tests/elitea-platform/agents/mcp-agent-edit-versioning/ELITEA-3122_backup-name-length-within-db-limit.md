---
id: ELITEA-3122
title: "Backup Version Name Length Stays Within the 128-Char DB Limit"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3122: Backup Version Name Length Stays Within the 128-Char DB Limit

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm the generated backup version name (`mcp-backup-{version_id}-{timestamp}`) stays within the database's 128-character version-name limit, including for a `version_id` with many digits.

---

## Preconditions

- Any sandbox agent/version; ideally one with a large numeric `version_id` if available.

---

## Test Data

| Field | Value |
|-------|-------|
| `version_id` | current sandbox version's actual ID (whatever digit count it naturally has) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Trigger a safe-patch edit creating a backup. | Backup created without a length-related DB error. |
| 2 | Measure the resulting backup name's character length. | ≤ 128 characters. |

---

## Expected Final State

No length-related failures for realistic `version_id` values.

---

## Actual Result — 2026-09-02

**Pass.** No length errors observed for any backup created this session (format `mcp-backup-<version_id>-<microsecond-UTC-timestamp>` comfortably fits within 128 chars for realistic version_id digit counts).

---

## Pass/Fail Criteria

**Pass:** No length-related DB error for realistic `version_id` values.
**Fail:** A DB error occurs due to the generated name exceeding 128 characters.
