---
id: ELITEA-1194
title: "Toolkit Test Settings — tools listed or blocked with explanation when credential is missing"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1194: Toolkit Test Settings — tools listed or blocked with explanation when credential is missing

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Test Settings panel on a toolkit with a missing credential shows either a blocked/error state or lists available tools — but does NOT silently show an empty/broken tool list with no explanation.

**Coverage:**
- Test Settings panel renders (not blank/broken) when credential is missing
- Tool dropdown either lists tools or shows a blocked state — never an unexplained empty list
- Running any tool returns a credential error, not a silent failure
- User can identify the cause of the failure from the Test Settings panel

## Preconditions

- Logged in to {{base_url}} as User B
- The GitHub toolkit has the credential error active (User B missing `test_github_credential`)
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Toolkit: GitHub toolkit with active missing-credential error
- Missing credential: `test_github_credential`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits. Open the GitHub toolkit with the active credential error. | Toolkit configuration page opens with the credential error visible. |
| 2 | Open the Test Settings panel (tool runner on the right side). | Test Settings panel renders — it is not blank or broken. |
| 3 | Open the Tool dropdown in Test Settings. | Either: (A) tools are listed in the dropdown, or (B) the panel shows a blocked/error state indicating the credential is missing. An unexplained empty dropdown is a failure. |
| 4 | If tools are listed (Option A), select any tool and click RUN TOOL. | Tool execution returns a credential error message referencing `test_github_credential`. There is no silent failure or generic unhandled error. |

## Expected Final State

Tool execution returns a credential error message referencing `test_github_credential`. There is no silent failure or generic unhandled error.

## Pass/Fail Criteria

**Pass:**
- Test Settings panel renders without being blank or broken
- Tool dropdown either lists tools OR shows an explicit blocked/error state
- Running a tool returns a credential error message referencing the missing credential name

**Fail:**
- Test Settings panel shows an empty tool list with no explanation
- Test Settings panel is completely blank or fails to render
- Running a tool produces a silent failure or generic unhandled error with no credential reference
