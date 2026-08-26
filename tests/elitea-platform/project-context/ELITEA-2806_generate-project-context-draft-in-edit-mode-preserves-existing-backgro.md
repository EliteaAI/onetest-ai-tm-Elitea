---
id: ELITEA-2806
title: "generate_project_context_draft in edit mode preserves existing background verbatim and appends only the requested section"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:generate_project_context_draft, edit-mode]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2806: generate_project_context_draft in edit mode preserves existing background verbatim and appends only the requested section

## Preconditions

- Test project (project_id 13) is accessible
- An existing markdown project background is available to pass as current_project_background

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "user_description": "Add an Accessibility Requirements section covering WCAG compliance.", "current_project_background": "<existing markdown background>"}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call generate_project_context_draft passing the existing current_project_background plus a targeted edit request | The response's markdown draft includes the original content preserved verbatim |
| 2 | Inspect the returned draft for the requested addition | Only the newly requested section (e.g. Accessibility Requirements) is appended; nothing else is rewritten, reordered, or removed |

## Expected Final State

Edit-mode drafting refines existing content incrementally instead of regenerating or rewriting it wholesale.

## Pass/Fail Criteria

**Pass:**
- Original content unchanged
- Only the requested new section is added

**Fail:**
- Any unrelated content is rewritten, reordered, or removed by an edit-mode request
