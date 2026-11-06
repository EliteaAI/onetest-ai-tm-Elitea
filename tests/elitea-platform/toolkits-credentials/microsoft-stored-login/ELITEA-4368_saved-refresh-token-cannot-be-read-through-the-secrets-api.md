---
id: ELITEA-4368
title: "[Parametrized] The saved Microsoft refresh token cannot be read back through the credential or secrets API by any project role"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7037, stored-login, security, secrets, data-exposure, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4368: [Parametrized] The saved Microsoft refresh token cannot be read back through the credential or secrets API by any project role

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Verify that nobody, including other admins, can get the raw refresh token of a saved Microsoft login. With the raw token, someone could act as the account directly at Microsoft for up to about 90 days, outside every ELITEA permission check.

**Why this is checked:** the code suggests this chain:
1. The credential GET returns `data.refresh_token` as a `{{secret.<id>}}` reference, which the UI uses to show **Logout**.
2. The token is stored as a *hidden* project secret under that `<id>`.
3. `GET /api/v2/secrets/secret/default/<project>/<id>` returns the plain value of a secret, including hidden ones, and is allowed for admins and editors by default.

If all three hold, the token leaks. Report any value returned in steps 3–4 as a security bug right away.

---

## Preconditions

- A team project **P** with users in each role: **ADM** (who saved the login), a second admin **ADM2**, an editor **ED** and a viewer **VW**.
- A Teams credential **C** in P with a login saved by ADM (ELITEA-4356 steps 1–2).
- An API client (for example Postman or curl) and a personal API token for each user.

---

## Test Data

| Variant | User |
|---|---|
| Second admin | ADM2 |
| Editor | ED |
| Viewer | VW |
| Saving admin | ADM |

Run steps 1–6 once per user.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send `GET {{base_url}}/api/v2/configurations/configuration/<project>/<C id>`. | The response does not contain the raw refresh token. Ideally it does not contain a `{{secret.<id>}}` reference either, only a flag such as `has_stored_login: true`. Note the `<id>` if a reference is returned. |
| 2 | Send `GET {{base_url}}/api/v2/configurations/configurations/<project>?type=teams` and check C's entry. | Same as step 1. |
| 3 | If step 1 returned `{{secret.<id>}}`, send `GET {{base_url}}/api/v2/secrets/secret/default/<project>/<id>`. | The request is refused (403 or 404), or returns an empty value. It **must not** return the refresh token value. |
| 4 | Send `GET {{base_url}}/api/v2/secrets/secrets/default/<project>` (list of secrets). | The stored-login secret is not listed, and no value is returned. |
| 5 | In the UI, open **Settings → Secrets** in P. Look for the stored-login secret and try to reveal it. | It is not shown and cannot be revealed. |
| 6 | Export C, or an agent that uses C, through any export / fork function available to the user. Open the exported file. | The file contains no refresh token value. |

---

## Expected Final State

No user, in any role, has the raw refresh token.

---

## Pass/Fail Criteria

**Pass:**
- In every variant, no step returns the refresh token value.

**Fail:**
- Any step returns the refresh token value, for any role. This is a critical security bug. Record the role, the request and the response, and stop using that login: log out and revoke MS-A's sessions at Microsoft.
