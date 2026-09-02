---
id: ELITEA-3096
title: "Backup Version Preserves Toolkit, Nested-Agent, Variable, and Tag Configuration"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3096: Backup Version Preserves Toolkit, Nested-Agent, Variable, and Tag Configuration

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm that a backup version created by an internal-MCP mutating call preserves the source version's selected toolkit mappings, nested-agent (pipeline agent) links, variables, and tags — the backup is a full config clone, not just an instructions snapshot.

---

## Preconditions

- Sandbox parent agent (#414) configured with at least one toolkit, one nested agent (#415), one variable, and one tag on its draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Nested agent | sandbox sub-agent (#415) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Record the source version's toolkit mappings, nested-agent link, variables, and tags (baseline). | Baseline captured. |
| 2 | Trigger an internal-MCP edit that creates a backup (e.g. a safe-patch instructions edit). | Backup version created. |
| 3 | Inspect the backup version's config. | Toolkit mappings, nested-agent link (#415), variables, and tag all present and identical to baseline. |

---

## Expected Final State

Backups are functionally complete snapshots of the pre-edit version, not partial copies.

---

## Actual Result — 2026-09-02

**Pass.** Verified on backup version #599 (cloned from agent #414's draft): toolkit mapping, nested sub-agent (#415) link, variable, and tag all preserved and matched the pre-edit source.

---

## Pass/Fail Criteria

**Pass:** All four configuration aspects preserved identically in the backup.
**Fail:** Any aspect (toolkit, nested-agent link, variable, tag) is missing, altered, or dropped in the backup.
