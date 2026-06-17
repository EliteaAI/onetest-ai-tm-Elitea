---
id: ELITEA-0949
title: "Editor Can Edit and Save Project Context — Private Project"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, editor-role, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0949: Editor Can Edit and Save Project Context — Private Project

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an Editor user can edit and save Project Context in a Private project.

**Coverage:**
- Editor can open editor, type, and save
- Content persists after reload and across sessions
- Private project scoped

## Preconditions

- Logged in as Editor user
- Private project accessible with Editor role assigned
- Project Context page navigable via Settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Editor. Go to Private project → Settings → Project Context. | Page loads with an editable editor field. |
| 2 | Type the text: 'QA context text by Editor'. Click Save. | Save succeeds. Success confirmation shown. No errors. |
| 3 | Reload the page. | Typed content is still present in the editor. |
| 4 | Close the browser completely, reopen, and navigate back to Project Context. | Content persists across browser sessions. |

## Expected Final State

Content persists across browser sessions.

## Pass/Fail Criteria

**Pass:**
- Editor can type and save content
- Content persists after reload and after browser restart

**Fail:**
- Editor field is read-only or save is blocked
- Content disappears after reload
