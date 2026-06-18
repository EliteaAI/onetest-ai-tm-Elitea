---
id: ELITEA-1181
title: "Verify Reload applies fixes of credentials Immediately"
priority: critical
type: functional
module: credential-actions-and-status-indicators
status: ready
execution_type: automated
tags: [feat:credentials, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5114]
---
# ELITEA-1181: Verify Reload applies fixes of credentials Immediately

**Module:** Credential Actions And Status Indicators · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the end-to-end flow — open an invalid credential via "Open in new tab", correct it, return to the toolkit view, click Reload, and confirm that both the Warning/Error icon and the authentication warning message disappear immediately.

**Coverage:**
- "Reload" tooltip present before action
- "Open in new tab" used to navigate to the credential for editing
- Credential fix applied and saved in the new tab
- Reload on return tab applies the credential changes without full page reload
- Warning/Error indicator clears after Reload
- Warning/authentication message clears after Reload

## Preconditions

- User logged into {{base_url}}
- A toolkit configured with an invalid credential that shows a Warning/Error indicator and an authentication warning message in the Toolkits area

## Test Data

| Field | Value |
|---|---|
| Toolkit | any toolkit showing authentication error on its credential row |
| Invalid credential | credential with wrong/expired token currently assigned to the toolkit |
| Corrected credential value | valid token/secret for the same credential type |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Toolkits area. | Toolkits list is displayed. |
| 2 | Locate the toolkit row with an invalid credential. Observe the credential row. | Warning/Error indicator (icon/badge) is visible. Authentication warning message is present. |
| 3 | Hover over the "Reload" icon on the credential row. | Tooltip appears with text matching the expected label (e.g., "Reload and apply changes"). Tooltip is not blank. |
| 4 | Click the "Open in new tab" icon on the same credential row. | A new browser tab opens with the credential detail/edit page. The original toolkit tab remains open and unchanged. |
| 5 | In the new tab, update the credential with correct, valid values and click Save. | Credential is saved successfully with valid values. |
| 6 | Switch back to the original toolkit tab (do not refresh the page). | Toolkit page is still showing the pre-fix state with the Warning/Error indicator and warning message. |
| 7 | Click the "Reload" icon on the credential row. | Page does not perform a full reload. Reload action completes cleanly with no spinner hang or error dialog. |
| 8 | Observe the credential row after Reload. | Warning/Error icon/badge is no longer displayed on the credential row. |
| 9 | Observe the authentication warning message area. | Warning/authentication message is no longer displayed. No residual error state remains on the row or toolkit card. |

## Expected Final State

Warning/authentication message is no longer displayed. No residual error state remains on the row or toolkit card.

## Pass/Fail Criteria

**Pass:**
- "Reload" tooltip is present and contains meaningful text
- "Open in new tab" opens the correct credential in a new browser tab
- After fixing the credential and clicking Reload, both the Warning/Error icon and the warning message disappear
- No full page reload is required
- No error dialog or spinner hang occurs

**Fail:**
- Tooltip is blank, missing, or shows a raw key
- "Open in new tab" does not open a new tab
- Warning/Error icon persists after Reload despite valid credential
- Warning message persists after Reload
- Full page reload is triggered
- Error dialog or infinite spinner appears
