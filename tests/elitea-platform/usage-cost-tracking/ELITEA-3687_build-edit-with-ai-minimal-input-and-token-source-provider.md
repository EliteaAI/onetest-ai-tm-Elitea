---
id: ELITEA-3687
title: "Build/Edit-with-AI minimal-input calls don't round to zero-cost; token_source is 'provider' not 'unparsed'"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, edit-with-ai, edge-case]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3687: Build/Edit-with-AI minimal-input calls don't round to zero-cost; token_source is 'provider' not 'unparsed'

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a minimal/very short Build-with-AI or Edit-with-AI invocation still records a non-zero-cost `usage_event` row, and that `token_source` is `'provider'` (not `'unparsed'`) for a normal successful call on a known model/endpoint.

---

## Preconditions

- Logged in to {{base_url}} with edit permission on an agent.

---

## Test Data

| Field | Value |
|-------|-------|
| Minimal description | A very short natural-language input, e.g. "Support bot" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke Build-with-AI with the minimal description above. | Call completes successfully, draft is generated. |
| 2 | Inspect the resulting `usage_event` row. | Input/output token counts are small but non-zero; cost is small but non-zero (not rounded to $0). |
| 3 | Inspect the row's `token_source` field. | `token_source` is `'provider'` — not `'unparsed'`. |

---

## Expected Final State

Minimal-input Build/Edit-with-AI calls still produce a correctly priced, non-zero row with `token_source='provider'`.

---

## Pass/Fail Criteria

**Pass:**
- Row has non-zero token counts and non-zero cost.
- `token_source='provider'`.

**Fail:**
- Row is missing, or shows zero cost for a real successful call.
- `token_source='unparsed'` on a known model/endpoint — file as a bug, not an edge case to ignore.
