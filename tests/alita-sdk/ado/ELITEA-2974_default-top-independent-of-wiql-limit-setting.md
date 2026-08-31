---
id: ELITEA-2974
title: "ADO Work Item Text Search – Default top=5 Is Independent of the Toolkit's Configured WIQL limit Setting"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, inconclusive]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2974: ADO Work Item Text Search – Default top=5 Is Independent of the Toolkit's Configured WIQL limit Setting

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the default result count (5) when `top` is omitted does not shift when the ADO Board toolkit's WIQL `limit` configuration setting is changed. **Status: previously untested — the toolkit's `limit` setting was never varied during exploratory testing; this is the first real pass at it.**

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- Admin/config access to change the toolkit's WIQL `limit` setting.
- A query matching more than 10 work items, so the default-vs-changed difference is observable.

---

## Test Data

| WIQL `limit` setting | Call | Expected `returned` |
|------------------------|------|------------------------|
| Default value | `search_work_items_by_text` with `top` omitted | `5` |
| Changed to a different value (e.g. 20) | `search_work_items_by_text` with `top` omitted | Still `5` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | With the toolkit's WIQL `limit` at its default, call with `top` omitted | `returned` is `5` (assuming ≥5 matches) |
| 2 | Change the toolkit's WIQL `limit` setting to a different value | Setting saved |
| 3 | Repeat the same call with `top` omitted | `returned` is still `5`, unaffected by the WIQL `limit` change |

---

## Expected Final State

The text search tool's own default `top` is independent of the WIQL tool's `limit` configuration.

---

## Pass/Fail Criteria

**Pass:** Default `returned` count stays at 5 regardless of the WIQL `limit` setting.
**Fail:** Changing the WIQL `limit` setting changes the text search tool's default result count.
