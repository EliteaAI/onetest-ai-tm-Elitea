---
id: ELITEA-0659
title: "Agent Import to Different Project — Correct Redirect"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3668]
---
# ELITEA-0659: Agent Import to Different Project — Correct Redirect

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that after importing an agent `.md` file into a different (non-active) project, the application correctly redirects the user to the newly imported agent detail page in that target project.

**Coverage:**
- Import wizard opens from the Agents section
- Project selector allows choosing a project different from the currently active one
- Import completes successfully when a non-active project is selected
- Post-import redirect navigates to the agent detail page in the correct (target) project
- Project indicator / breadcrumb reflects the target project after redirect
- No error messages or broken navigation occur

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- At least two projects exist and the user has access to both (Project A and Project B)
- Project A is set as the currently active / open project
- A previously exported agent `.md` file is available for upload
- Browser: any modern Chromium-based browser

## Test Data

- **Active project:** Project A (any project the user currently has open)
- **Target project:** Project B (a different project — must not be the currently active one)
- **Import file:** valid agent export file in `.md` format (e.g., `test-agent-export.md`)
- **Expected redirect URL pattern:** `.../app/[project-b-id]/agents/[new-agent-id]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a valid agent .md export file. | File is ready for upload. |
| 2 | Open Project A and confirm it is the currently active project (check project indicator / breadcrumb). | Project A is open and shown as the active project. |
| 3 | Navigate to the Agents section from the left sidebar. | Agents list page for Project A is displayed. |
| 4 | Click the Import button. | Import wizard dialog opens. |
| 5 | Upload the agent .md file. | File is accepted; wizard advances to the project selection step. |
| 6 | In the project selector dropdown, choose Project B (different from Project A). | Project B is selected as the import target. |
| 7 | Click Import / confirm the import. | Import process starts; a loading/progress indicator is shown. |
| 8 | Wait for the import to complete. | Success state is displayed with a 'Got it' button visible. |
| 9 | Click 'Got it'. | Wizard closes. |
| 10 | Observe the page the application navigates to. | App redirects to the newly imported agent detail page. |
| 11 | Check the project indicator / breadcrumb in the header. | Project B is shown as the active project context. |
| 12 | Check for any error messages, toast notifications, or broken UI elements. | No errors or warnings are present; agent detail page loads fully. |

## Expected Final State

No errors or warnings are present; agent detail page loads fully.

## Pass/Fail Criteria

**Pass:**
- After clicking 'Got it', the app redirects to the agent detail page in Project B
- Project B is reflected in the project indicator / breadcrumb
- No error messages or toast warnings appear
- Agent detail page renders fully without broken UI

**Fail:**
- App redirects to Project A (the previously active project) instead of Project B
- A "not found" or access error page is shown after redirect
- Redirect does not happen at all — user stays on the import wizard or agents list
- Any error message or exception is displayed
