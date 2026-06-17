---
id: ELITEA-1071
title: "[EliteaAI/elitea_issues#5116] Refresh Icon Reloads Secrets List Without Closing Dropdown"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-1071: [EliteaAI/elitea_issues#5116] Refresh Icon Reloads Secrets List Without Closing Dropdown

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the refresh icon in the SAVED SECRETS header reloads the list in-place — the dropdown remains open and no page navigation occurs.

**Note:** No existing OneTest coverage found for this specific behavior. This is new coverage.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has secret create/list permissions
- A credential creation/edit form is open with a token field in Secret mode
- At least one secret already exists in the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the secret dropdown on a credential token field in Secret mode. | Dropdown is open showing CREATE section and SAVED SECRETS list. |
| 2 | Note the current count and names of secrets listed in the SAVED SECRETS section. | Baseline secret list recorded. |
| 3 | Without closing the dropdown, open a separate browser tab manually (not via the shortcut) and navigate to Settings → Secrets in the same project. Create a new secret (e.g., tc5116_refresh_check) and save it with ✓. | New secret saved successfully in the separate tab. |
| 4 | Switch back to the credential form tab. Verify the dropdown is still open. | Dropdown is still open (was not closed by switching tabs). |
| 5 | Click the refresh icon in the SAVED SECRETS section header. | (1) The dropdown remains open — it does not collapse or close. (2) tc5116_refresh_check appears in the SAVED SECRETS list. (3) No page reload or navigation occurs. (4) All previously listed secrets are still present with no duplicates. (5) The CREATE section is still visible above SAVED SECRETS. |

## Expected Final State

(1) The dropdown remains open — it does not collapse or close. (2) tc5116_refresh_check appears in the SAVED SECRETS list. (3) No page reload or navigation occurs. (4) All previously listed secrets are still present with no duplicates. (5) The CREATE section is still visible above SAVED SECRETS.

## Pass/Fail Criteria

**Pass:** Dropdown stays open after refresh; new secret appears in list; no duplicates; no page navigation.
**Fail:** Dropdown collapses on clicking refresh; new secret not loaded; page reloads or navigates; duplicate entries appear in the list.
