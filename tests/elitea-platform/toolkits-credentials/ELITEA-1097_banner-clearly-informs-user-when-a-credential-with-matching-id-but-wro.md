---
id: ELITEA-1097
title: "Banner clearly informs user when a credential with matching ID but wrong type exists"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1097: Banner clearly informs user when a credential with matching ID but wrong type exists

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user has a private credential with the same ID as required but of a different type, the warning banner clearly communicates the type mismatch rather than a generic "credential missing" message, and the "Create a credential" link pre-selects the correct type.

**Coverage:**
- Type-mismatch scenario (same ID, wrong credential type)
- Banner message accuracy for type mismatch
- Pre-filled credential creation with correct type

## Preconditions

- Team project toolkit type: **Jira**, required private credential ID: `team_integration`
- **User B** has a private credential with ID `team_integration` but of type **GitHub** (wrong type)

## Test Data

- Toolkit type: Jira
- Required credential ID: `team_integration`
- User B's existing private credential: ID=`team_integration`, Type=GitHub

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and open the Jira team toolkit → Configuration tab. | Configuration form is shown. |
| 2 | Observe the warning banner. | A warning banner is shown. |
| 3 | Read the banner message carefully. | Banner clearly indicates that the credential type is mismatched — it specifies that a **Jira** credential is required, not just that a credential is missing. |
| 4 | Verify the banner does **not** state the credential is simply "absent" or "not found". | Message acknowledges a type mismatch, not a complete absence. |
| 5 | Click the **"Create a credential"** link in the banner. | A new tab opens with the credential creation form. |
| 6 | Verify the credential type on the creation form. | Credential type is pre-selected as **Jira** (not GitHub). |

## Expected Final State

Credential type is pre-selected as **Jira** (not GitHub).

## Pass/Fail Criteria

**Pass:**
- Banner message specifically communicates the type mismatch (not just credential missing)
- "Create a credential" link opens with Jira type pre-selected
- Message is accurate and not misleading

**Fail:**
- Banner shows generic "credential not found" message that does not mention type mismatch
- "Create a credential" link pre-selects GitHub (wrong type)
- Banner is absent despite the type mismatch condition
