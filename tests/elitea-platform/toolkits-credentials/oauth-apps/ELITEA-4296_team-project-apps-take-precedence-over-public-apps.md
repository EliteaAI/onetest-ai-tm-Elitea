---
id: ELITEA-4296
title: "Team project's own OAuth apps take precedence over Public apps, per credential type"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:admin-platform, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4296: Team project's own OAuth apps take precedence over Public apps, per credential type

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify the tier rule: when a team project has any enabled app for a credential type, Public apps are ignored there for that type, even a Public Default. Other projects and personal projects keep the Public tier.

---

## Preconditions

- App **PUB**: Public, **Default**, all 3 types.
- App **TEAM**: pr_A only, **not** Default, all 3 types.
- User U1 is editor in pr_A and pr_B (pr_B has no own app) and has a personal project.
- U1 has an Outlook credential **C_PUB** in pr_A saved on PUB **before** TEAM was enabled (enable TEAM after creating it).

---

## Test Data

| Project | Expected for Outlook |
|---------|----------------------|
| pr_A | TEAM only, switcher |
| pr_B | PUB Default, no switcher |
| Personal | PUB Default, no switcher |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1 in **pr_A**, New → Outlook. | Default app / Custom app switcher; no picker; TEAM is used. PUB is not offered. API `?type=outlook` → only TEAM, `mode: "choice"`. |
| 2 | In **pr_B**, New → Outlook. | No switcher: PUB Default. API → only PUB, `mode: "default"`. |
| 3 | In the **personal** project, New → Outlook. | Same as pr_B (Public tier). |
| 4 | In pr_A, open **C_PUB**. | Error "The Microsoft Entra ID app selected for this credential is not available in this project. Switch to Custom app." The app name is not shown. |
| 5 | Run an agent in pr_A with C_PUB's toolkit. | Run fails with the same message. |
| 6 | As Admin, switch **Outlook off** on TEAM. As U1 in pr_A, New → Outlook. | PUB Default applies again (no switcher). New → **Teams** in pr_A still shows TEAM (switcher). |
| 7 | Reopen C_PUB. | Works again (no error). |
| 8 | Switch Outlook on for TEAM. **Disable** TEAM. In pr_A New → Outlook. | PUB Default applies (no project-tier apps left). |
| 9 | Enable TEAM. As a user of a third project pr_C, New → Teams. | TEAM is not offered there; PUB applies. |
| 10 | **Record (R6, not built):** U1 creates a Default Outlook credential in the **personal** project, adds the toolkit to an agent in **pr_A**, and runs it. | Spec: resolves through Public (PUB). Note which app's client ID is used (sign-in prompt / Network). If TEAM is used, report (checklist G5). |

---

## Postconditions

- Disable TEAM, delete test credentials.
