---
id: ELITEA-4709
title: "Node YAML View — Rename via id, Validation Errors and Invalid YAML Handling"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7158]
---
# ELITEA-4709: Node YAML View — Rename via id, Validation Errors and Invalid YAML Handling

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify renaming via `id`, rejection of duplicate/empty `id` and `type` changes, inline handling of invalid YAML, and the Fix / Discard YAML Changes prompt when switching to Flow or closing the panel.

**Coverage:**
- `id` rename; live card update while typing
- Duplicate `id`, empty `id`, `type` change errors (exact texts)
- Save disabled while any error is shown
- Invalid YAML: inline error, nothing applied, page Yaml unaffected
- Fix / Discard YAML Changes on Flow switch and on panel close
- Known: elitea_issues#7408 — renaming does not update other nodes' references (enhancement, out of scope)
- See ELITEA-4717 for the main flow

## Preconditions

- Logged in to {{base_url}}
- A pipeline with nodes `LLM Node` and `Code Node` connected to each other

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open LLM Node's YAML tab; change `id` to `LLM renamed`. | The node is renamed; the card updates live while typing. |
| 2 | Change `id` to `Code Node` (existing). | Error below the editor: *"The name has been used by other nodes, please input a new name!"*; not applied; Save disabled. |
| 3 | Clear `id` completely. | Error *"Name is required"*; the card keeps its previous name; Save disabled. Typing a valid name resumes live updates. |
| 4 | Change `type` to another value (also try via Ctrl+H Replace). | Error *"Node type can't be changed in the node YAML."*; not applied; Save disabled. |
| 5 | Introduce a syntax error (e.g. break indentation of a multi-line key). | Inline error, e.g. *"Invalid YAML: can not read a block mapping entry; a multiline key may not be an implicit key."*; nothing applied; the page Yaml is unchanged; Save disabled. |
| 6 | With the invalid YAML, click the **Flow** toggle. | Modal *"Invalid node YAML — The node YAML has errors, so it wasn't applied. Fix it, or discard your YAML changes to go back to the last valid version."* with **Fix** / **Discard YAML Changes**. |
| 7 | Click **Fix**. | Modal closes; stays in YAML with the error shown. |
| 8 | Click ✕ to close the panel. | The same modal appears. |
| 9 | Click **Discard YAML Changes**. | The node YAML reverts to the last valid version; no partial changes. |
| 10 | After the rename in step 1, observe the edge from Code Node. | Known: elitea_issues#7408 — references in other nodes are not updated (connection disappears until reselected). Not a failure of this case. |

## Expected Final State

Invalid node YAML is never applied; every validation error shows its exact message and keeps Save disabled; the Fix / Discard prompt protects against leaving with invalid YAML.

## Pass/Fail Criteria

**Pass:**
- Rename works; duplicate/empty `id` and `type` change rejected with exact messages
- Save disabled while any error is shown
- Invalid YAML not applied; prompt appears on Flow switch and close; Discard reverts cleanly

**Fail:**
- An invalid change is applied, or Save is enabled during an error
- Prompt missing on Flow switch or close
- Discard leaves partial changes
