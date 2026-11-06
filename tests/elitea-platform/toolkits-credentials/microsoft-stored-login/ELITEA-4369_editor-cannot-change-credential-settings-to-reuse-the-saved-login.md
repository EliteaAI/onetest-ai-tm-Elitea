---
id: ELITEA-4369
title: "[Parametrized] An editor cannot change the client, scopes or endpoint of a team credential and keep using its saved Microsoft login"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7037, stored-login, security, privilege-escalation, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4369: [Parametrized] An editor cannot change the client, scopes or endpoint of a team credential and keep using its saved Microsoft login

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Verify that a non-admin cannot widen what the admin's saved login can do by editing the credential's other fields. The server's admin-only check covers changes to `refresh_token` itself; this case checks the fields next to it. Expected safe behaviour, either:
- changing these fields on a credential with a saved login is refused for non-admins, **or**
- the change is allowed but removes the saved login.

---

## Preconditions

- A team project **P** with admin **ADM** and editor **ED**.
- A Teams credential **C** with a login saved by ADM for **MS-A**, with scopes `ChannelMessage.Read.All`, `User.Read`.
- MS-A has also consented to a wider scope such as `Chat.ReadWrite` or `Mail.Read` for the same Entra app (so a scope change could succeed).
- A Teams toolkit **T** using C, and an agent **AG** with T attached.
- A second Entra app **APP2** with its own client ID and secret.

---

## Test Data

| Variant | Field ED changes on C |
|---|---|
| Scopes | Add `Chat.ReadWrite` (or `Mail.Read`) to the scopes |
| Client ID / secret | Replace with APP2's |
| Discovery endpoint | Change to another tenant: `https://login.microsoftonline.com/<other_tenant>` |
| Non-Microsoft endpoint | Change to `https://example.com/<tenant>` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, open C and change the field from the variant. Click **Save**. Also try the same change with `PUT {{base_url}}/api/v2/configurations/configuration/<project>/<C id>`, keeping `refresh_token` unchanged. | Either the save is refused for ED, or it succeeds and the saved login is removed (`data.refresh_token` is gone and C shows not connected). |
| 2 | If the save succeeded and `refresh_token` is still there, ask AG to use the toolkit (for example list chats, or read email for the Mail variant). | The tool must not return data from MS-A's account beyond the originally saved scopes. |
| 3 | For the **Non-Microsoft endpoint** variant, check the save result. | The save is refused with a message that the endpoint must be `https://login.microsoftonline.com/<tenant_id>`. No request with the token reaches `example.com`. |
| 4 | As ADM, reload C. | If C was changed, ADM can see what changed. The saved login is either intact with the original settings, or removed. |

---

## Expected Final State

The saved login can only be used with the settings ADM saved it with.

---

## Pass/Fail Criteria

**Pass:**
- For every variant, ED cannot keep the saved login while changing these fields, or the change has no effect on what the login can reach.
- The non-Microsoft endpoint is refused.

**Fail:**
- ED saves the change, `refresh_token` stays, and a run then reaches MS-A's data with wider scopes, a different app or a different tenant. This is a privilege escalation bug.
