---
id: ELITEA-4295
title: "User creates a working Teams, Outlook or SharePoint toolkit with the Default app and no app credentials"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:oauth, int:teams, int:outlook, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4295: User creates a working Teams, Outlook or SharePoint toolkit with the Default app and no app credentials

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the main acceptance criterion: a user saves a credential with only a name, signs in with Microsoft through the admin app, and an agent uses the toolkit. The secret never reaches the browser, the scope is locked to the admin's, and sign-ins stay per user.

---

## Preconditions

- App **PUB** (Public, Default, valid secret, all 3 types, recommended scopes, SharePoint scopes `User.Read Sites.Read.All`).
- Users **U1** and **U2**, editors in team project pr_B (no own apps). Each has a Microsoft account in the app's tenant with a mailbox, Teams and a SharePoint site.
- An agent **AG_4295** in pr_B.

---

## Test Data

| Toolkit | Prompt | Expected tool |
|---------|--------|---------------|
| Outlook | "Read my 3 latest emails" | read mail |
| Teams | "List my Teams chats" | list chats |
| SharePoint | "List the lists on site <url>" | get lists |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1 in pr_B, Credentials → New → **Outlook**. | No switcher, "Sign-in settings are managed by your administrator.". Save is **disabled** before typing. |
| 2 | Enter a name `OL_U1_4295` and Save. | Saved, back to the list. **No** "unsaved changes" warning. |
| 3 | GET the credential via API. | `data.oauth_app_id` = PUB's uuid. No client_id/secret/endpoint/scopes stored by the user (any client fields in the read come from the app; no secret). |
| 4 | Reopen the credential, then leave without edits. | No warning on leave. |
| 5 | Create an Outlook toolkit with this credential, add it to AG_4295. | Saved. |
| 6 | Open the toolkit's sign-in (Configuration OAuth window). | Scope is **read-only**, shows PUB's Outlook scopes, tooltip "Set by your administrator for the default app." |
| 7 | Open DevTools Network. Sign in with U1's Microsoft account. | Microsoft consent shows the app's name and the admin scopes. Sign-in succeeds. The request to `/elitea_core/mcp_oauth_proxy/{pr_B}` has `oauth_app_id` and `credential_type: "outlook"` and **no** client secret. The response has tokens and **no** secret. |
| 8 | In a chat with AG_4295, send the Outlook prompt. | The tool runs and returns U1's emails. |
| 9 | Run the credential's **Test connection**. | Returns a sign-in prompt / status with the app's client ID; no secret, not even masked. |
| 10 | Repeat 1 – 8 for **Teams** and **SharePoint**. | Both work the same. |
| 11 | As U2, create own Outlook credential and toolkit the same way and sign in with U2's account. Run the prompt. | U2 sees **U2's** emails. U1's chat still shows U1's emails: sign-ins are per credential. |
| 12 | As U1, create a **Custom** Outlook credential in a project with no Default (or check one existing) and open its sign-in. | Scope is **editable** there. |

---

## Postconditions

- Delete the toolkits and credentials.
