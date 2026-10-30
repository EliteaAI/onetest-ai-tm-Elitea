---
id: ELITEA-1967
title: "Credential — Type-Specific Form Fields (Core Types)"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1967: Credential — Type-Specific Form Fields

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting the most frequently used credential types renders the correct set of type-specific form fields, auth method options, and Test connection button state. This test covers a representative sample of the platform's credential types for regression validation.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential types under test | GitHub, SharePoint, Confluence, Jira |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new credential type "GitHub" | Fields shown: Display Name, ID (disabled), Base Url (pre-filled "https://api.github.com"), Auth radio (Anonymous, Token, Password, App private key); Test connection enabled |
| 2 | Create new credential type "SharePoint" | Fields shown: Display Name, ID, Client Id, Client Secret (Secret/Password toggle), Site Url, Auth radio (App-only, Delegated); Test connection enabled |
| 3 | Create new credential type "Confluence" | Fields shown: Display Name, ID, Hosting dropdown (Auto), Base Url, Auth radio (Basic, Bearer), Api Key (Secret/Password toggle), Username; Test connection enabled |
| 4 | Create new credential type "Jira" | Fields shown: Display Name, ID, Hosting dropdown (Auto), Base Url, Auth radio (Basic, Bearer), Api Key (Secret/Password toggle), Username; Test connection enabled |

---

## Expected Final State

Each of the core credential types (GitHub, SharePoint, Confluence, Jira) presents its correct set of fields, auth options, and Test connection button state as defined in the platform specification.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each credential type renders exactly the expected fields, auth options, and Test connection state.

**Fail:**
- Any step produces an error or unexpected result.
- A credential type shows incorrect, missing, or extra fields compared to the specification.

---

## Notes

**Regression scope:** This test validates the 4 most frequently used credential types for core regression. Additional credential types (ADO, GitLab, Figma, Postman, Langfuse, Report Portal) are validated in extended/pre-release testing to balance regression coverage with manual execution efficiency.

**Full coverage available in:** Extended test suite or pre-release validation for all 10+ supported credential types.
