---
id: ELITEA-3088
title: "Safe-Patch Call Against a Published or Embedded Version Is Rejected"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3088: Safe-Patch Call Against a Published or Embedded Version Is Rejected

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a safe-patch call targeting a version whose status is `published` or `embedded` is rejected with 409 (`VersionNotUpdatableError`), with no backup created and no change applied. **Blocked this session** — no published/embedded version was available in the sandbox to target.

---

## Preconditions

- An agent version in `published` or `embedded` status.

---

## Test Data

| Field | Value |
|-------|-------|
| Version status | `published` (and, separately, `embedded`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Publish (or embed) a version of a test agent. | Version status becomes `published`/`embedded`. |
| 2 | Attempt a safe-patch call against that version, with a correct current hash. | 409 (`VersionNotUpdatableError`). |
| 3 | Re-read the version. | Unchanged. |
| 4 | List versions. | No new backup created. |

---

## Expected Final State

Published/embedded versions remain immutable via the safe patch tool, same as via direct edits.

---

## Actual Result — 2026-09-02

**Not tested this session.** No published or embedded version existed in the sandbox project to target. Requires publishing/embedding a disposable test version first.

---

## Pass/Fail Criteria

**Pass:** 409 `VersionNotUpdatableError` for both `published` and `embedded`, zero side effects.
**Fail:** Patch succeeds against an immutable version.

---

## Blocked / Fixture Needed

Requires a sandbox agent with a version explicitly published or embedded before execution.
