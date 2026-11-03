---
id: ELITEA-4364
title: "A saved Microsoft login revoked at Microsoft makes runs ask for a login, without crashing the run"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7037, stored-login, p1]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4364: A saved Microsoft login revoked at Microsoft makes runs ask for a login, without crashing the run

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify what happens when the saved refresh token stops working at Microsoft: the toolkit asks for a login, the rest of the run continues, and the credential shows that the login is no longer valid.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A Teams credential **C** with a login saved for **MS-A**, and a toolkit **T** using it.
- A pipeline **PL** whose first node calls a Teams tool through T and whose second node is a plain LLM node.
- Access to MS-A's Microsoft account settings.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run PL. | Both nodes complete and the Teams node returns data. |
| 2 | At Microsoft, revoke MS-A's sessions: **My Account → Sign out everywhere**, or change MS-A's password. | — |
| 3 | Wait at least 1 hour, so the cached access token expires. Run PL from a schedule with no browser open. | The Teams node reports that a login is needed (authorization required). The run does not crash with an internal error, and the LLM node still runs if the pipeline allows it. |
| 4 | Open T. | The bar shows that the saved login is no longer valid (**Not Connected** or a login prompt). |
| 5 | On C, log in again as MS-A and run PL. | PL completes with data again. |

---

## Expected Final State

After a new login, PL works. While the login was revoked, the run failed only in the Teams node and showed a login prompt.

---

## Pass/Fail Criteria

**Pass:**
- Step 3 shows a login or authorization prompt in the Teams node, and the run ends cleanly.

**Fail:**
- The run fails with a raw stack trace, or hangs.
- The run keeps using the revoked account.
