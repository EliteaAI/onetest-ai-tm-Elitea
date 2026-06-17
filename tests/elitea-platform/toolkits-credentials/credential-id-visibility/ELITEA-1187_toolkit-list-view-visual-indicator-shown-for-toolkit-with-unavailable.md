---
id: ELITEA-1187
title: "Toolkit list view — visual indicator shown for toolkit with unavailable credential"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1187: Toolkit list view — visual indicator shown for toolkit with unavailable credential

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that on the Toolkits list page, a toolkit with a credential error is visually differentiated (e.g., warning icon, error badge) so the user can identify problematic toolkits before opening them.

**Coverage:**
- Toolkit card with missing credential shows a visual warning indicator (icon or badge)
- Toolkit card with valid credential shows no such indicator
- Hovering the indicator (if present) reveals a tooltip or description including the credential name/ID

## Preconditions

- Logged in to {{base_url}} as User B
- At least one toolkit has an active credential unavailability error (missing `test_github_credential`)
- At least one toolkit has a valid credential visible to User B
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Broken toolkit: GitHub toolkit referencing `test_github_credential` (unavailable to User B)
- Healthy toolkit: any toolkit where User B owns the required credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Toolkits (list view). | Toolkits list page displays toolkit cards. |
| 2 | Locate the GitHub toolkit card with the missing credential. | A visual indicator (warning icon ⚠, red badge, or error state) is visible on the toolkit card. |
| 3 | Locate a toolkit card where User B owns the required credential. | No warning indicator is shown on the healthy toolkit card. |
| 4 | Hover over the warning indicator on the broken toolkit card (if it is a hoverable element). | A tooltip or description appears confirming the credential issue, including the credential name `test_github_credential`. |

## Expected Final State

A tooltip or description appears confirming the credential issue, including the credential name `test_github_credential`.

## Pass/Fail Criteria

**Pass:**
- Broken toolkit card shows a visual warning indicator
- Healthy toolkit card shows no warning indicator
- Hovering the indicator reveals credential name in tooltip or description

**Fail:**
- No visual indicator distinguishes the broken toolkit from healthy toolkits in list view
- Tooltip or hover text does not include the credential name
