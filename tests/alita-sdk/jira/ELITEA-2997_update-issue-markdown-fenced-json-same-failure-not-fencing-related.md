---
id: ELITEA-2997
title: "Jira update_issue (SDK) – Markdown-Fenced JSON Payload Fails Identically, Confirming the Bug Is Downstream of #5856's Fence-Unwrapping Logic"
priority: critical
type: functional
module: jira
status: draft
execution_type: manual
tags: [sdk, jira, update-issue, adf, issue:5856, bug]
requirements: [EliteaAI/elitea_issues#5856]
---

# ELITEA-2997: Jira update_issue (SDK) – Markdown-Fenced JSON Payload Fails Identically, Confirming the Bug Is Downstream of #5856's Fence-Unwrapping Logic

**Module:** Jira · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that wrapping the exact same payload from [[ELITEA-2996]] in a markdown JSON fence (` ```json ... ``` `) produces the identical `HTTPError: Operation value must be a string` failure — confirming that #5856's fence-stripping/unwrapping normalization is not the differentiator, and the crash occurs downstream of payload parsing (i.e. in the `update=` operations-format construction/submission, not in normalization).

---

## Preconditions

- Jira toolkit is configured with valid credentials against a Cloud v3 (ADF-capable) deployment.
- A test issue exists (e.g. `CRM-142`) that can be safely updated.
- [[ELITEA-2996]] has been run so the unfenced-payload baseline failure is confirmed for comparison.

---

## Test Data

| Field | Value |
|-------|-------|
| Issue key | `CRM-142` |
| Method | `update_issue` (SDK) |
| Payload (markdown-fenced) | ` ```json\n{"key": "CRM-142", "fields": {"description": {"type":"doc","version":1,"content":[{"type":"paragraph","content":[{"type":"text","text":"Line one"},{"type":"hardBreak"},{"type":"text","text":"Line two"}]}]}}}\n``` ` (identical JSON to [[ELITEA-2996]], wrapped in a markdown code fence) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `update_issue` (SDK) for `CRM-142` with the markdown-fenced payload above | Call either succeeds, or fails with a clear, sanitized validation error |
| 2 | Compare the resulting error (if any) against the unfenced-payload result from [[ELITEA-2996]] | Behavior is identical between fenced and unfenced variants |
| 3 | Confirm the fence itself was correctly stripped before any downstream processing (i.e. the failure, if any, is not a fence-parsing error) | No fence-related parsing error; if it fails, it fails with the same downstream error as the unfenced case |

---

## Expected Final State

Fenced and unfenced variants of the same payload behave identically — proving fence-stripping is not the source of the failure, and any remaining defect is downstream (in `update=` operations-format handling).

---

## Pass/Fail Criteria

**Pass:** Fenced payload behaves identically to the unfenced payload (both succeed, or both fail with the exact same sanitized/clean error).
**Fail:** Fenced payload reproduces the same raw `HTTPError: Operation value must be a string` traceback as the unfenced case (as currently observed — Run 2 of the #5856 investigation, confirming the crash is not fixed by fence-handling alone).
