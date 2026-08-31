---
id: ELITEA-2970
title: "ADO Work Item Text Search – Each Result Contains Only the Documented Minimal Field Set (No Body/Comments/Relations Leak)"
priority: critical
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, data-safety]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2970: ADO Work Item Text Search – Each Result Contains Only the Documented Minimal Field Set (No Body/Comments/Relations Leak)

**Module:** Ado · **Priority:** Critical · **Type:** Functional

**Objective:** Verify every result object contains only `id`, `title`, `type`, `state`, `project`, `url`, and optional `assigned_to` — and never leaks `description`/`body`/`comments`/`relations`/`attachments` or raw ADO `fields`.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- At least one matching work item has a long description, comments, and relations/attachments set, to make any leak detectable.

---

## Test Data

| Field | Value |
|-------|-------|
| query | A term matching a work item that has a description, comments, and at least one relation/attachment |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with the query above | Call succeeds |
| 2 | Enumerate every key present on the matching result object | Only the documented field set is present |
| 3 | Explicitly check for `description`, `body`, `comments`, `relations`, `attachments`, and any raw `fields` object | None of these keys are present |

---

## Expected Final State

No result ever exposes full work item body content, comments, relations, or raw ADO field payloads.

---

## Pass/Fail Criteria

**Pass:** Every result strictly matches the documented minimal field set.
**Fail:** Any undocumented field — especially description/body/comments/relations/attachments/raw fields — appears on any result.
