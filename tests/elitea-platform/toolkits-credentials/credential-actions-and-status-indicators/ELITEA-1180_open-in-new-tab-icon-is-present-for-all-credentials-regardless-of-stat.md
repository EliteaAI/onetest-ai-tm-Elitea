---
id: ELITEA-1180
title: "\"Open in new tab\" icon is present for all credentials regardless of status, shows a tooltip, and opens the credential in a new tab — Toolkits area"
priority: critical
type: functional
module: credential-actions-and-status-indicators
status: ready
execution_type: automated
tags: [feat:credentials, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5114]
---
# ELITEA-1180: "Open in new tab" icon is present for all credentials regardless of status, shows a tooltip, and opens the credential in a new tab — Toolkits area

**Module:** Credential Actions And Status Indicators · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Open in new tab" icon is visible on every credential row regardless of status, provides a tooltip on hover, and opens the correct credential in a new tab; also confirm no false-positive Warning/Error badge appears on valid credentials.

**Coverage:**
- Icon visible for valid credentials
- Icon visible for invalid/expired credentials
- Tooltip present and readable
- Click on invalid credential opens correct credential in new tab
- Original tab remains open
- No Warning/Error badge shown for valid credential (false-positive check)

## Preconditions

- User logged into {{base_url}}
- At least one toolkit with a valid credential and one with an invalid/expired credential visible in the Toolkits area
- Multi-tab browser environment

## Test Data

| Field | Value |
|---|---|
| Valid credential toolkit | any toolkit with successfully authenticated credential |
| Invalid credential toolkit | any toolkit showing authentication error or missing credential |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits from the sidebar. | Toolkits list is displayed. |
| 2 | Locate a toolkit row referencing a valid credential. Observe the credential entry. | "Open in new tab" icon is visible on the valid credential entry. |
| 3 | Hover over the "Open in new tab" icon on the valid credential entry. | Tooltip appears. Text matches expected label (e.g., "Open in new tab") and is not blank or a raw key/ID. |
| 4 | Locate a toolkit row referencing an invalid or expired credential. Observe the credential entry. | "Open in new tab" icon is also visible on the invalid credential entry (icon is not hidden or disabled for invalid credentials). |
| 5 | Click the "Open in new tab" icon on the invalid credential row. | A new browser tab opens. The original tab remains open and unchanged. |
| 6 | In the new tab, observe the content. | The correct credential (matching name/ID) is displayed in its detail or edit view. |
| 7 | Return to the original tab. Locate the valid credential row again. Confirm no Warning or Error icon/badge is displayed on it. | No Warning/Error badge shown for the valid credential. "Open in new tab" icon is still visible. |

## Expected Final State

No Warning/Error badge shown for the valid credential. "Open in new tab" icon is still visible.

## Pass/Fail Criteria

**Pass:**
- "Open in new tab" icon visible for both valid and invalid credentials
- Tooltip present with meaningful text
- Clicking the icon on an invalid credential opens the correct credential in a new browser tab
- Original tab remains open
- No Warning/Error badge shown for valid credential

**Fail:**
- Icon missing or hidden for any credential regardless of status
- Tooltip blank, missing, or shows a raw internal key
- Click does not open a new tab
- New tab shows wrong or empty credential page
- Warning/Error badge shown for a valid, working credential (false positive)
