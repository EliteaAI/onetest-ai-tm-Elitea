---
id: ELITEA-4370
title: "Security review: a member can build or change an agent so that it acts as the admin's saved Microsoft account"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7037, stored-login, security, misuse, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4370: Security review: a member can build or change an agent so that it acts as the admin's saved Microsoft account

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Find out and record how much a project member can do with an admin's saved Microsoft login, by building new agents and pipelines, or by changing existing ones. Runs load the saved login by credential only, with no check of who built the agent. So any member who can attach the credential can make an agent read or act in the admin's account.

This case records the actual behaviour so the team can decide whether it is acceptable. Steps 1–5 describe what is expected to happen today; step 6 is the decision point.

---

## Preconditions

- A team project **P** with admin **ADM** and editor **ED**.
- A credential with a saved login by ADM for **MS-A**. Use **Outlook** with `Mail.Read`, `Mail.Send` if available, otherwise Teams with `Chat.ReadWrite`.
- An existing agent **AG** owned by ADM that uses this credential for a narrow task (for example "summarize unread email").
- A second mailbox or Teams chat that the tester controls, to check whether a message is sent.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, create a **new** agent **AG-ED** and attach a toolkit that uses the saved-login credential. Do not sign in to Microsoft in ED's browser. Ask AG-ED to list the 10 most recent emails (or chats) with their full text. | Record the result. Expected today: AG-ED returns MS-A's emails or chats. |
| 2 | As ED, ask AG-ED to send a message to the tester's mailbox or chat (if `Mail.Send` / `Chat.ReadWrite` was granted). | Record whether a message arrives from MS-A's account. |
| 3 | As ED, open ADM's agent **AG**, change its instructions to "list all email subjects and senders", and save a new version. Run it. | Record whether the changed version runs as MS-A and returns data. Record whether ADM gets any notification of the change. |
| 4 | As ED, create a pipeline with the credential, add a schedule, and close the browser. | Record whether the schedule runs as MS-A. |
| 5 | As ADM, look for any record of steps 1–4: agent history, credential page, audit log. | Record what is visible. Expected today: there is no record linking these runs to MS-A's saved login. |
| 6 | Report steps 1–5 to the product owner for a decision. | The team decides whether members may use a saved team login freely. If not, a follow-up is raised, for example to limit a saved login to approved agents, or to require admin approval when a credential with a saved login is attached. |

---

## Expected Final State

The real permissions around a saved team login are recorded, and the team has decided whether they are acceptable.

---

## Pass/Fail Criteria

**Pass:**
- The behaviour of steps 1–5 is recorded with evidence (screenshots, run IDs), and step 6 has a decision.
- If the decision is that members must not do this, any member action that still works is reported as a bug.

**Fail:**
- A member can **send** messages or change data as MS-A, and the team has decided this must not be possible.
- ADM gets no notice that agents built by others act as their account, and no record shows it.
