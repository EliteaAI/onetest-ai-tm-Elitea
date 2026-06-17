---
id: ELITEA-0956
title: "Editor/Admin Can Edit and Save Project Context in Editor Mode — Team Project"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, persistence, story:3395, issue:3395, edit-mode, r-2.0.4, admin]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0956: Editor/Admin Can Edit and Save Project Context in Editor Mode — Team Project

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an Admin user can edit, type in, and save Project Context content in both Private and Team projects.

**Coverage:**
- Admin opens editor in Edit mode
- Admin types content and saves
- Saved content persists after page reload
- Edit applies in both Private and Team projects

## Preconditions

- Logged in as Admin user
- Private project and Team project both accessible
- Project Context page navigable via Settings

## Test Data

- Test content: '# QA Project Context

Stack: TypeScript, React.
Team rule: Always cite sources.'
- Admin user credentials
- Both Private and Team project IDs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Admin. Open a Private project → Settings → Project Context. | Project Context page loads with an editable editor. |
| 2 | Click inside the editor area. Verify the cursor is active and the field is editable. | Editor accepts keyboard input; cursor is visible. |
| 3 | Type the following content: '# QA Project Context\n\nStack: TypeScript, React.\nTeam rule: Always cite sources.' | Text appears in the editor as typed. |
| 4 | Click Save (or the equivalent save button). | Save succeeds with a success toast/confirmation. No errors displayed. |
| 5 | Reload the page (F5 or browser refresh). | The previously saved content is still present in the editor after reload. |
| 6 | Repeat steps 1–5 for a Team project. | Admin can also edit and save Project Context in a Team project. Content persists. |
| 7 | Close the browser and reopen the Project Context page. | Content is still present (persists across browser sessions). |

## Expected Final State

Content is still present (persists across browser sessions).

## Pass/Fail Criteria

**Pass:**
- Admin can type content in the editor
- Save succeeds without errors
- Content is present after page reload
- Applies to both Private and Team projects

**Fail:**
- Editor is not editable for Admin
- Save button is absent or non-functional
- Content is lost after reload
