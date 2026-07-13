---
id: ELITEA-1967
title: "Credential — Type-Specific Form Fields"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1967: Credential — Type-Specific Form Fields

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting each supported credential type renders the correct set of type-specific form fields, auth method options, and Test connection button state.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential types under test | GitHub, SharePoint, ADO, GitLab, Confluence, Jira, Figma, Postman, Langfuse, Report Portal |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new credential type "GitHub" | Fields shown: Display Name, ID (disabled), Base Url (pre-filled "https://api.github.com"), Auth radio (Anonymous, Token, Password, App private key); Test connection enabled |
| 2 | Create new credential type "SharePoint" | Fields shown: Display Name, ID, Client Id, Client Secret (Secret/Password toggle), Site Url, Auth radio (App-only, Delegated); Test connection enabled |
| 3 | Create new credential type "ADO" | Fields shown: Display Name, ID, Organization Url, Token (Secret/Password toggle); no Auth radio; Test connection enabled |
| 4 | Create new credential type "GitLab" | Fields shown: Display Name, ID, Url, Auth radio (GitLab private token only), Private Token (Secret/Password toggle); Test connection enabled |
| 5 | Create new credential type "Confluence" | Fields shown: Display Name, ID, Hosting dropdown (Auto), Base Url, Auth radio (Basic, Bearer), Api Key (Secret/Password toggle), Username; Test connection enabled |
| 6 | Create new credential type "Jira" | Fields shown: Display Name, ID, Hosting dropdown (Auto), Base Url, Auth radio (Basic, Bearer), Api Key (Secret/Password toggle), Username; Test connection enabled |
| 7 | Create new credential type "Figma" | Fields shown: Display Name, ID, Auth radio (Token only), Token (Secret/Password toggle); Test connection enabled |
| 8 | Create new credential type "Postman" | Fields shown: Display Name, ID, Base Url, Workspace Id, Auth radio (API Key only), Api Key (Secret/Password toggle); Test connection DISABLED |
| 9 | Create new credential type "Langfuse" | Fields shown: Display Name, ID, Base URL, Public Key, Secret Key (Secret/Password toggle); no Auth radio; Test connection enabled |
| 10 | Create new credential type "Report Portal" | Fields shown: Display Name, ID, Project, Endpoint, Api Key (Secret/Password toggle); no Auth radio; Test connection enabled |

---

## Expected Final State

Each credential type presents its correct set of fields, auth options, and Test connection button state as defined in the platform specification.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each credential type renders exactly the expected fields, auth options, and Test connection state.

**Fail:**
- Any step produces an error or unexpected result.
- A credential type shows incorrect, missing, or extra fields compared to the specification.
