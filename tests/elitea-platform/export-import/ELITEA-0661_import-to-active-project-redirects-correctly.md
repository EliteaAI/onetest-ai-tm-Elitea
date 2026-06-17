---
id: ELITEA-0661
title: "Import to Active Project Redirects Correctly"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3668]
---
# ELITEA-0661: Import to Active Project Redirects Correctly

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that importing an agent or pipeline `.md` file into the same currently active project still produces the correct post-import redirect after the fix for cross-project redirect (issue #3668) is applied.

**Coverage:**
- Same-project import flow for both agents and pipelines remains unbroken after the cross-project fix
- Post-import redirect still navigates to the correct entity detail page within the same project
- No regression is introduced in the default (same-project) import flow
- Project context does not change unexpectedly after a same-project import

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- At least one project exists and the user has write access to it (Project A)
- Project A is set as the currently active / open project
- A previously exported agent `.md` file and a previously exported pipeline `.md` file are both available for upload
- Browser: any modern Chromium-based browser

## Test Data

- **Active project (=target project):** Project A — the same project for both import operations
- **Agent import file:** valid agent export in `.md` format (e.g., `test-agent-same-project.md`)
- **Pipeline import file:** valid pipeline export in `.md` format (e.g., `test-pipeline-same-project.md`)
- **Expected redirect URL pattern (agent):** `.../app/[project-a-id]/agents/[new-agent-id]`
- **Expected redirect URL pattern (pipeline):** `.../app/[project-a-id]/pipelines/[new-pipeline-id]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a valid agent .md export file. | File is ready for upload. |
| 2 | Open Project A and confirm it is the currently active project. | Project A is open and shown as the active project. |
| 3 | Navigate to Agents → click Import. | Import wizard opens. |
| 4 | Upload the agent .md file. | File accepted; wizard advances to the project selection step. |
| 5 | In the project selector, select Project A (the same project that is currently open). | Project A is selected as the import target. |
| 6 | Click Import / confirm. | Import runs successfully. |
| 7 | Click 'Got it' on the success dialog. | Wizard closes; app redirects to the imported agent detail page within Project A. Project A remains the active project. No errors appear. |
| 8 | Prepare a valid pipeline .md export file. | File is ready for upload. |
| 9 | Navigate to Pipelines → click Import, upload the pipeline .md file, select Project A in the project selector, click Import, then click 'Got it'. | App redirects to the newly imported pipeline detail page within Project A. Project A remains the active project. No errors appear. |

## Expected Final State

App redirects to the newly imported pipeline detail page within Project A. Project A remains the active project. No errors appear.

## Pass/Fail Criteria

**Pass:**
- Agent import to same project redirects to the correct agent detail page in Project A
- Pipeline import to same project redirects to the correct pipeline detail page in Project A
- Project A remains the active project throughout both operations
- No errors or unexpected behavior occur

**Fail:**
- Redirect fails or points to the wrong project after any same-project import
- Error page or "not found" message appears after clicking 'Got it'
- Active project context changes unexpectedly
- Any error message is displayed
