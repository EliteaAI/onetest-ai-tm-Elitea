---
id: ELITEA-1895
title: "Export agent with nested agent dependencies — produces .zip archive"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1895: Export agent with nested agent dependencies — produces .zip archive

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that exporting an agent that has nested agent dependencies produces a .zip archive containing multiple .md files — one per entity.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with at least one nested agent attached exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent that has at least one nested agent attached | The agent detail page loads |
| 2 | Click three-dot menu → "Export" | The export action is triggered |
| 3 | Verify a .zip file is downloaded | A .zip file download is initiated |
| 4 | Extract the archive and verify it contains multiple .md files (one per entity) | The extracted archive contains at least two .md files (main agent + nested agent(s)) |

---

## Expected Final State

The exported .zip archive contains multiple .md files, one for the main agent and one for each nested agent dependency.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- A .zip file is downloaded and contains multiple .md files (one per entity).

**Fail:**
- Any step produces an error or unexpected result.
- A .md file is downloaded instead of a .zip, or the archive does not contain files for all entities.
