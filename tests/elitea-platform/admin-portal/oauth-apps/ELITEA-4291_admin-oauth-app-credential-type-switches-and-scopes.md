---
id: ELITEA-4291
title: "Admin Portal OAuth app: credential type switches and scopes control what users get"
priority: high
type: functional
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, feat:credentials, int:teams, int:outlook, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4291: Admin Portal OAuth app: credential type switches and scopes control what users get

**Module:** admin-portal/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify the Teams / Outlook / SharePoint switches and scopes in the app dialog: at least one type must stay on, scopes of a switched-off type are kept, and a type switched off stops offering the app to that type's credentials only.

---

## Preconditions

- Admin user. App `OA_Test_4289` (not Default) assigned to team project **pr_A**, no other app for pr_A.
- User **U1** is an editor in pr_A.

---

## Test Data

| Field | Value |
|-------|-------|
| Teams extra scope | ChatMessage.Send |
| SharePoint scopes | `User.Read, Sites.Read.All` |
| Unknown type (API) | `"scopes": {"jira": ["read"]}` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Edit the app. Check ChatMessage.Send in Teams. Type `User.Read, Sites.Read.All` in SharePoint. Save. | Saved. Reopen: ChatMessage.Send checked; SharePoint shows `User.Read Sites.Read.All` (comma split into 2 scopes). |
| 2 | Switch **Teams** off. | Teams scopes are hidden. Text "Off: Teams credentials cannot use this app." |
| 3 | Switch Outlook and SharePoint off too. | Save and Test connection are **disabled**. |
| 4 | Send the same by API: PUT with `credential_types: []`. | 400 "Enable at least one credential type for this app". |
| 5 | Switch Outlook and SharePoint on again, keep Teams off, Save. | List row Credentials column shows only **Outlook** and **SharePoint** chips. |
| 6 | As U1 in pr_A, open Credentials → New → **Teams**. | Plain Custom app form: no Default/Custom switcher (the app isn't offered for Teams). |
| 7 | As U1, open New → **Outlook**. | Default app / Custom app switcher is shown. |
| 8 | As Admin, switch Teams on again and open the scopes. | The Teams scopes come back as saved in step 1 (ChatMessage.Send still checked). |
| 9 | Uncheck all Outlook scopes and Save. | Saved. At the next Outlook sign-in (ELITEA-4295) the recommended set (Mail.Read) is requested. |
| 10 | API PUT with `"scopes": {"jira": ["read"]}`. | 400 "Microsoft Entra ID apps have no scopes for: jira". |
| 11 | API PUT with `"credential_types": ["teams", "jira"]`. | 400 "Microsoft Entra ID apps cannot serve: jira". |

---

## Postconditions

- Restore all 3 types on and the recommended scopes.
