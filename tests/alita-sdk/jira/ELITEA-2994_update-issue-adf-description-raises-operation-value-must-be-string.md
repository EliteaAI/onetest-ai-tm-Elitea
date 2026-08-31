---
id: ELITEA-2994
title: "Jira update_issue (SDK) – ADF description (heading + bold paragraph + bullet list) raises 'Operation value must be a string'"
priority: critical
type: functional
module: jira
status: draft
execution_type: manual
tags: [sdk, jira, update-issue, adf, issue:5856, bug]
requirements: [EliteaAI/elitea_issues#5856]
---

# ELITEA-2994: Jira update_issue (SDK) – ADF description (heading + bold paragraph + bullet list) raises 'Operation value must be a string'

**Module:** Jira · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that calling the SDK `update_issue` method with an ADF `description` payload containing an H2 heading, a bold paragraph, and a bullet list does not fail with an unhandled `HTTPError: Operation value must be a string`, and does not leak a raw internal traceback to the caller.

---

## Preconditions

- Jira toolkit is configured with valid credentials against a Cloud v3 (ADF-capable) deployment.
- A test issue exists (e.g. `CRM-5`) that can be safely updated.

---

## Test Data

| Field | Value |
|-------|-------|
| Issue key | `CRM-5` |
| Method | `update_issue` (SDK) |
| description (ADF) | Document containing: one `heading` node (level 2), one `paragraph` node with a bold `text` mark, one `bulletList` node with at least one `listItem` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call the SDK `update_issue` method for `CRM-5` with the ADF `description` payload described above (heading + bold paragraph + bullet list), submitted via the SDK's `update=` operations-format routing | Call either succeeds (issue updated) or fails with a clear, user-facing validation error |
| 2 | Inspect the error/response returned to the caller | No raw `HTTPError` traceback or internal file paths are surfaced to the caller |
| 3 | If the call failed, re-read the issue to confirm no partial/corrupt update occurred | Issue description is unchanged from before the failed call |

---

## Expected Final State

The SDK either successfully applies the ADF description update, or fails with a clear, sanitized validation error — never a raw `HTTPError: Operation value must be a string` traceback.

---

## Pass/Fail Criteria

**Pass:** Update succeeds, or fails with a clear, non-leaking validation error message.
**Fail:** Call raises `HTTPError: Operation value must be a string` with a raw internal traceback surfaced to the caller (as currently observed — this is the tracked bug for #5856).
