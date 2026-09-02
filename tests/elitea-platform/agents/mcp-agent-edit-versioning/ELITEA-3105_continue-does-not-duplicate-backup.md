---
id: ELITEA-3105
title: "\"Continue\" After a Completed Edit Does Not Duplicate the Backup or Re-Apply the Patch"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, chat, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3105: "Continue" After a Completed Edit Does Not Duplicate the Backup or Re-Apply the Patch

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that if a safe-patch edit completes successfully and the user then sends "Continue" (e.g. out of habit, or because the AI reply itself was truncated after the tool call succeeded), no duplicate backup is created and the already-applied patch is not silently re-attempted. **Not testable from this session** — requires the same hard-to-reproduce truncation timing as [[ELITEA-3104]], specifically truncation of the AI's *text reply* after a tool call has already succeeded.

---

## Preconditions

- A completed, successful safe-patch edit whose confirmatory AI text reply is then truncated.

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario | Tool call succeeds; AI's follow-up text reply is truncated before finishing |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Perform a successful safe-patch edit; confirm one backup created and hash updated. | Baseline confirmed. |
| 2 | Truncate the AI's confirmatory text reply (simulated or naturally occurring). | Reply cut off, but mutation already committed. |
| 3 | Send "Continue". | No second backup created; instructions/hash unchanged from step 1's post-edit state. |

---

## Expected Final State

Exactly one backup and one applied patch persist; "Continue" causes no additional mutation.

---

## Actual Result — 2026-09-02

**Not testable from this session.** Same reproducibility constraint as [[ELITEA-3104]] — could not reliably force a truncated AI text reply immediately following a successfully committed tool call within the sandbox session.

---

## Pass/Fail Criteria

**Pass:** No duplicate backup or re-applied patch after "Continue" following a completed edit.
**Fail:** A second backup appears, or the patch is re-applied (e.g. double-replacement), after "Continue".

---

## Blocked / Fixture Needed

Requires reliably reproducing a truncated AI text reply immediately after a successful tool-call commit.
