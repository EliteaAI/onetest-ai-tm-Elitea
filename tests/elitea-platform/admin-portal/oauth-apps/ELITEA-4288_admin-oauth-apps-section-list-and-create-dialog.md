---
id: ELITEA-4288
title: "Admin Portal OAuth Apps: section, list and create dialog"
priority: high
type: functional
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, feat:credentials, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4288: Admin Portal OAuth Apps: section, list and create dialog

**Module:** admin-portal/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify that a platform admin can open Configuration → OAuth Apps, see the list with the right columns and create a Microsoft Entra ID app with the dialog defaults, required fields and recommended scopes.

---

## Preconditions

- User **Admin** has the Administration `admin` or `super_admin` role.
- A real Entra ID app registration: client ID, client secret value, tenant ID.
- A team project **pr_A** exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Name | `OA_Test_4288` |
| Client ID | Client ID of the test Entra app |
| Client secret | Secret value of the test Entra app |
| Endpoint | `https://login.microsoftonline.com/` + tenant ID of the test Entra app |
| Projects | pr_A |
| Long name | 129 characters |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin, open Admin Portal → Configuration. | **OAuth Apps** is listed right after MCP Servers, with an icon. |
| 2 | Open OAuth Apps. | The section opens with no "Unexpected Application Error". The description text explains Default app, Custom app and "at most one Default app" per provider. No shared Save/Discard bar is shown. |
| 3 | If the list is empty, note the empty state. | "No apps yet. Users can still bring their own app (Custom app)." (Skip if the seeded Elitea default app exists.) |
| 4 | Click **New Configuration for App**. | Dialog "New OAuth app" opens. General block: Provider, Name, Enabled, Default app, Projects. |
| 5 | Check the Provider field. | "Microsoft Entra ID", **disabled**, helper "Identity provider of this app. Only Microsoft Entra ID is available." |
| 6 | Check the defaults. | Enabled **on**. Default app **off**. Projects empty, shown red, helper "Required. The app applies only in the selected projects." Endpoint `https://login.microsoftonline.com/organizations`. Teams, Outlook and SharePoint switches **on**. Auto refresh token **on**. |
| 7 | Check the preselected scopes. | Teams: User.ReadBasic.All, Chat.Read, Team.ReadBasic.All, Channel.ReadBasic.All checked; ChatMessage.Send, Chat.Create, ChannelMessage.Send unchecked. Outlook: only Mail.Read checked. SharePoint: empty text field with helper "Space separated Microsoft Graph scopes". |
| 8 | Check Save and Test connection. | Both are **disabled**. |
| 9 | Fill Name, Client ID, Client secret and endpoint, leave Projects empty. | Save and Test connection stay disabled. |
| 10 | Open the Projects picker and type part of "pr_A". | The list filters. Select pr_A: it shows as a chip "pr_A (ID: …)". Save becomes enabled. |
| 11 | Replace the name with a 129-character name and click Save. | Save fails with an error in the dialog: "Name must not exceed 128 characters". |
| 12 | Set the name back to `OA_Test_4288` and click Save. | Dialog closes. Toast "App created.". |
| 13 | Check the new row. | Name `OA_Test_4288`, Provider "Microsoft Entra ID", Client ID, chips Teams / Outlook / SharePoint, Projects "1 selected", Status "Enabled". Edit and delete icons are on one line. |
| 14 | Hover the name. | Tooltip shows the discovery endpoint. |

---

## Postconditions

- Keep `OA_Test_4288` for ELITEA-4289 – 4291, or delete it.
