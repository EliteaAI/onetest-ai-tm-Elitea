---
id: ELITEA-1957
title: "Remote MCP — Cache TTL Configuration"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1957: Remote MCP — Cache TTL Configuration

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Cache TTL field on a Remote MCP can be changed from its default value, saved, and that the new value is persisted in the Raw JSON.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.

---

## Test Data

| Field | Value |
|-------|-------|
| Default Cache TTL | 300 |
| New Cache TTL | 600 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Verify "Cache TTL" field shows default 300 | Field shows 300 |
| 3 | Verify info icon is present | Info icon is visible next to Cache TTL label |
| 4 | Change Cache TTL to 600 | Field displays 600 |
| 5 | Save MCP | Operation completes successfully |
| 6 | Reload — verify Cache TTL is 600 | Cache TTL field shows 600 after reload |
| 7 | Switch to Raw Json — verify "cache_ttl": 600 | JSON shows cache_ttl as 600 |

---

## Expected Final State

The Cache TTL value is updated to 600, persisted after reload, and reflected correctly in the Raw JSON.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cache TTL change is persisted and reflected in Raw JSON.

**Fail:**
- Any step produces an error or unexpected result.
- Cache TTL value is not persisted or Raw JSON does not reflect the change.
