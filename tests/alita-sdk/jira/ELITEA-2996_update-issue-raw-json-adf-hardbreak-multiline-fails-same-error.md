---
id: ELITEA-2996
title: "Jira update_issue (SDK) – Raw JSON ADF Description With hardBreak/Multiline Fails With Identical Error and Leaks Internal Paths"
priority: critical
type: functional
module: jira
status: draft
execution_type: manual
tags: [sdk, jira, update-issue, adf, issue:5856, bug]
requirements: [EliteaAI/elitea_issues#5856]
---

# ELITEA-2996: Jira update_issue (SDK) – Raw JSON ADF Description With hardBreak/Multiline Fails With Identical Error and Leaks Internal Paths

**Module:** Jira · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that calling `update_issue` (SDK) with a raw (unfenced) JSON payload of the shape `{"key": "<issue>", "fields": {"description": <ADF doc>}}`, where the ADF description is a single paragraph containing a `hardBreak` node and two lines of text, reproduces the same `HTTPError: Operation value must be a string` failure as [[ELITEA-2994]], and confirm whether the traceback surfaced includes internal file paths.

---

## Preconditions

- Jira toolkit is configured with valid credentials against a Cloud v3 (ADF-capable) deployment.
- A test issue exists (e.g. `CRM-142`) that can be safely updated.

---

## Test Data

| Field | Value |
|-------|-------|
| Issue key | `CRM-142` |
| Method | `update_issue` (SDK) |
| Payload (raw, unfenced) | `{"key": "CRM-142", "fields": {"description": {"type":"doc","version":1,"content":[{"type":"paragraph","content":[{"type":"text","text":"Line one"},{"type":"hardBreak"},{"type":"text","text":"Line two"}]}]}}}` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `update_issue` (SDK) for `CRM-142` with the raw JSON payload above (not markdown-fenced) | Call either succeeds, or fails with a clear, sanitized validation error |
| 2 | Inspect the exact error text/traceback returned to the caller | No internal file paths, stack frames, or raw `HTTPError` details are exposed |
| 3 | Re-read `CRM-142` to confirm no partial update occurred if the call failed | Description unchanged from before the call |

---

## Expected Final State

The raw-JSON ADF payload with `hardBreak`/multiline content either updates successfully or fails cleanly, with no internal traceback or file-path leakage.

---

## Pass/Fail Criteria

**Pass:** Update succeeds, or fails with a clean, sanitized error containing no internal paths/stack details.
**Fail:** Call raises `HTTPError: Operation value must be a string` with a full internal traceback (including file paths) surfaced to the caller — as currently observed (Run 1 of the #5856 investigation).
