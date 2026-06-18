---
id: ELITEA-1139
title: "Verify credential used by a toolkit can be deleted with proper handling"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials]
requirements: []
---
# ELITEA-1139: Verify credential used by a toolkit can be deleted with proper handling

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Users cannot delete a credential that is currently referenced by one or more toolkits. The system either silently fails, shows an unhelpful error, or blocks deletion without clearly indicating which toolkits depend on the credential and what actions are needed.

## Preconditions

User is logged into Elitea platform
User has permission to manage credentials and toolkits
At least one credential exists that is actively used by a toolkit
User has access to both Credentials and Toolkits pages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page and identify a toolkit that uses a specific credential (note the credential name) | Toolkit is found with an associated credential identified in its configuration |
| 2 | Navigate to Credentials page and locate the credential identified in step 1 | Credential is listed on the Credentials page with its details visible |
| 3 | Attempt to delete the credential that is used by the toolkit (click delete button/action) | System either: (a) shows a clear warning listing dependent toolkits and asks for confirmation, OR (b) provides an informative error explaining the dependency |
| 4 | If a warning dialog appears, verify it lists the specific toolkit(s) that depend on this credential | Warning message clearly identifies which toolkit(s) use this credential, e.g., 'Used by: My GitHub Toolkit' |
| 5 | If deletion is blocked, navigate to the dependent toolkit and remove or change its credential reference | Toolkit can be updated to use a different credential or have the credential reference removed |
| 6 | Return to Credentials page and attempt to delete the credential again (now with no dependencies) | Credential is successfully deleted without errors |
| 7 | Verify the credential no longer appears in the Credentials list | Deleted credential is removed from the list. Page shows updated credential count |
| 8 | Navigate to the toolkit that previously used the deleted credential and verify its state | Toolkit either shows no credential configured or indicates the credential needs to be re-configured |
| 9 | Attempt to use the toolkit (e.g., run a tool in Test Settings) that had its credential deleted without reconfiguring a new credential | Toolkit operation fails with a clear error message indicating missing credentials — no silent failure, no generic 500 error. The error message guides the user to reconfigure the credential |
| 10 | Create a credential that is referenced by TWO different toolkits simultaneously. Attempt to delete it and verify the warning lists BOTH dependent toolkits | Warning/error message lists both dependent toolkits by name — not just the first one found. User is informed of the full scope of the dependency |
| 11 | If the system allows forced deletion of a credential with dependencies, verify that all dependent toolkits are properly updated to reflect the missing credential (navigate to each toolkit) | All dependent toolkits show a clear indication that their credential is missing/invalid. No toolkit appears to still have a valid credential reference to the deleted credential |
| 12 | Check if an agent that was using one of the affected toolkits still loads correctly on its detail page (no crash or blank page) | Agent detail page loads without crashing. The affected toolkit section may show a warning about missing credentials, but the page remains functional and other agent settings are accessible |

## Expected Final State

Agent detail page loads without crashing. The affected toolkit section may show a warning about missing credentials, but the page remains functional and other agent settings are accessible

## Pass/Fail Criteria

PASS: System provides clear feedback about credential dependencies listing all affected toolkits, allows deletion after resolving dependencies, toolkit shows actionable missing-credential state, tool execution fails with clear error, agent pages remain stable
FAIL: Deletion silently fails, shows a generic/unhelpful error, succeeds without warning leaving toolkits in a broken state, dependency warning misses some toolkits, post-deletion toolkit gives cryptic error, or agent page crashes
