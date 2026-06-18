---
id: ELITEA-1070
title: "[EliteaAI/elitea_issues#5116] Full E2E: Create Secret via Shortcut, Refresh, Select, and Save Credential (Private + Team)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-1070: [EliteaAI/elitea_issues#5116] Full E2E: Create Secret via Shortcut, Refresh, Select, and Save Credential (Private + Team)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify the complete end-to-end flow in both project contexts: use the "New Secret" shortcut → create secret → return → refresh dropdown → select new secret → save credential → verify authentication succeeds.

**Test Data (Parametrized):**

| # | Project Type | New Secret Name | Button Label | Auth Expected |
|---|---|---|---|---|
| A | Private | `tc5116_private_token` | "New Private Secret" | GitHub API success |
| B | Team | `tc5116_team_token` | "New Project Secret" | GitHub API success |

*If GitHub is not applicable, use any other toolkit with a token/secret field (e.g., Jira or Confluence) and an appropriate token.*

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has credential and secret create/list permissions
- Access to both a private project and a team project
- A valid GitHub personal access token (PAT) available for testing

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In the target project (row A = private, row B = team), navigate to Configuration → Credentials → Create Credential → GitHub. | GitHub credential creation form opens. |
| 2 | Fill in Display Name (e.g., TC-5116-[ProjectType]). Set Base URL to https://api.github.com. Select Token auth type. | Form fields populated. |
| 3 | Switch the token field to Secret mode. Open the secret dropdown. | Dropdown opens showing CREATE section with the correct label and SAVED SECRETS section. |
| 4 | Verify the credential form data (Display Name, Base URL) is still intact with the dropdown open. | Form data preserved while dropdown is open. |
| 5 | Click 'New Private Secret' (row A) or 'New Project Secret' (row B) from the CREATE section. | A new browser tab opens with Settings → Secrets page for the correct project. |
| 6 | In the new tab, verify the creation input row is already active. Enter the secret name from the parameter table and paste the valid GitHub PAT as value. Save with ✓. | Secret saved successfully. Creation row was auto-open (no manual '+' needed). New secret appears in the Secrets list. |
| 7 | Switch back to the credential form tab. | Credential form still shows all entered data (Display Name, Token auth type, Secret mode) — no data loss. |
| 8 | Click the refresh icon in the SAVED SECRETS section header of the dropdown. | The new secret (e.g., tc5116_private_token) appears in the SAVED SECRETS list, exactly once, with no duplicates. |
| 9 | Select the new secret from the SAVED SECRETS list. | Secret is selected; its name appears in the combobox. |
| 10 | Click Save on the credential form. | Credential saved successfully. |
| 11 | Click Test Connection on the saved credential. | Test Connection returns success (HTTP 200 / success indicator from GitHub API) — not a 'secret not found' or 'invalid token' error. |

## Expected Final State

Test Connection returns success (HTTP 200 / success indicator from GitHub API) — not a 'secret not found' or 'invalid token' error.

## Pass/Fail Criteria

**Pass:** Both parameter rows (A and B) complete all steps successfully and end with a successful API authentication.
**Fail:** Form data lost on tab return; refresh does not load new secret; duplicate entries appear after refresh; credential fails to save; connection test fails with 'secret not found' or auth error.
