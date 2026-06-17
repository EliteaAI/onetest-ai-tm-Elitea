---
id: ELITEA-1074
title: "[#5116] \"New Private Secret\" Shortcut Visible in Credential Secret Dropdown (Private Project)"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-1074: [#5116] "New Private Secret" Shortcut Visible in Credential Secret Dropdown (Private Project)

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in a private project, the credential secret dropdown shows a CREATE section with the label "New Private Secret" plus a refresh icon in the SAVED SECRETS section.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has `configuration.secrets.secret.create` and `configuration.secrets.secret.list` permissions (at least editor role)
- A private project is accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Configuration → Credentials in a private project. | Credentials list page loads successfully. |
| 2 | Click Create Credential and select the GitHub credential type. (If GitHub is not available, any toolkit type with a token/secret field — e.g., Jira or Confluence — is acceptable.) | Credential creation form opens. |
| 3 | In the auth section, select Token auth type. | Token field is visible. |
| 4 | Click the Secret toggle to switch the token field to Secret mode. | Token field switches to Secret mode; a combobox/dropdown appears for secret selection. |
| 5 | Open the secret selection dropdown (click the combobox). | Dropdown opens and shows: (1) a CREATE section at the top with the label 'New Private Secret'; (2) a SAVED SECRETS section below (may be empty); (3) a refresh icon next to the SAVED SECRETS section header. |

## Expected Final State

Dropdown opens and shows: (1) a CREATE section at the top with the label 'New Private Secret'; (2) a SAVED SECRETS section below (may be empty); (3) a refresh icon next to the SAVED SECRETS section header.

## Pass/Fail Criteria

**Pass:** Dropdown shows CREATE section labeled exactly "New Private Secret" and a refresh icon in the SAVED SECRETS header.
**Fail:** CREATE section missing; label says "New Project Secret" (wrong scope); refresh icon absent; dropdown shows no structured sections.
