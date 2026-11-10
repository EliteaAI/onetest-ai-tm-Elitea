---
id: ELITEA-4568
title: "Dataverse toolkit — create: credential picker, read / write tool groups, selected tools, warning on open"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, issue:7471]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7471"]
---

# ELITEA-4568: Dataverse toolkit — create: credential picker, read / write tool groups, selected tools, warning on open

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify creating a Dataverse toolkit: the credential picker, the five tools in the read and write groups, the selected tools reaching the agent, and the warning shown on opening a toolkit or agent without a login.

**Known:** [#7471](https://github.com/EliteaAI/elitea_issues/issues/7471) (enhancement): "Sign in to Dataverse to connect this credential." is shown each time a toolkit or agent is opened without a login.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved.
- A second, private Dataverse credential.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Toolkits → **+ Create** → **Dataverse (OneCRM)**. | Credential picker lists only Dataverse credentials (team and private). |
| 2 | Open the tools list. | 5 tools: group **read** (who_am_i, get_record, query_records, describe_entity) and group **write** (update_record). Group select / deselect works. |
| 3 | Select only the read group; save. Add T to an agent and ask it to update a record. | The agent has no update_record tool and says so. |
| 4 | Select no tool; save. **Record** which tools the agent gets. | All tools (an empty selection means all). |
| 5 | Switch T to the private credential. | The Login bar shows that credential's state. |
| 6 | Open T, then an agent with T (no login). | **Record** the warning "Sign in to Dataverse to connect this credential." (#7471: should not be shown; the Login bar is enough). |

---

## Expected Final State

T exists with all tools and C.

---

## Pass/Fail Criteria

**Pass:**
- Tools, groups and the credential picker behave as above.

**Fail:**
- A tool is missing or in the wrong group.
- Deselected tools are still available to the agent.
