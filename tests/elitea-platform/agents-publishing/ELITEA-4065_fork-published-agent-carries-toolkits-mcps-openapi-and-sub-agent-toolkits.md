---
id: ELITEA-4065
title: "Forking a published agent carries its toolkits, MCPs and OpenAPI, including sub-agents' toolkits"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:import-forking, feat:toolkits, issue:6859, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#6859"]
---

# ELITEA-4065: Forking a published agent carries its toolkits, MCPs and OpenAPI, including sub-agents' toolkits

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that forking a published agent from the Catalog brings along every toolkit attached to the published version: native toolkits, remote MCPs, local MCPs and OpenAPI. Each sub-agent must bring its own toolkits too. Settings and selected tools must be preserved, and no manual re-attachment may be needed. The Catalog copy must still show and run no toolkits, and the toolkit data stored on it must not expose secrets.

**Out of scope:** pipelines (separate enhancement), credential names, agents published before the fix.

---

## Preconditions

- Two users: **Author** (editor in project **P-Author**) and **Forker** (editor in project **P-Fork**, a different project).
- Publishing to the Catalog is enabled for P-Author. AI publish validation is enabled.
- The agents in this test are published **after** the #6859 fix was deployed.
- In P-Author, a 3-tier agent:
  - **Orchestrator** has 1 native toolkit with only **part** of its tools selected, and 1 native toolkit with an **index** (vector store + index schedule). Internal tools are enabled and a step limit is set.
  - Its sub-agent **Secondary** has 1 **OpenAPI** toolkit (spec + secret header, 2 operations selected) and 1 **remote MCP** (URL, one sensitive header such as `Authorization`, and one ordinary header such as `X-Client-Name`).
  - Secondary's sub-agent **Leaf** has 1 native toolkit and 1 **local MCP** that is connected in Author's environment.
- Forker has **not** added the corresponding local MCP yet.
- A Keycloak JWT for a **third user** who is not a member of P-Author.

---

## Test Data

| Field | Value |
|-------|-------|
| Tier 1 | Orchestrator: native toolkit (tool subset) + indexed native toolkit |
| Tier 2 | Secondary: OpenAPI + remote MCP |
| Tier 3 | Leaf: native toolkit + local MCP |
| Instructions without fallback (step 1) | "Always use the toolkit to look up the item before answering." |
| Fallback text (step 3) | "If the toolkit is not available, explain what is needed and answer from general knowledge." |

---

## Steps

### Part A: Publish and the Catalog copy

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, put the no-fallback instructions on Orchestrator and on Leaf. Start publishing Orchestrator and run the AI validation. | Rule 9 "Toolkit Dependencies" shows a **warning** for the main agent's `instructions`, **and** a warning for the sub-agent, labelled with its name. The LLM writes the wording, so it varies between runs. |
| 2 | Note the warning wording. | Record whether it says toolkits "will not be included after publishing". That is misleading now that forks include them. |
| 3 | Add the fallback text to both agents and validate again. | No Toolkit Dependencies warning for either agent. |
| 4 | Publish. | Published. Secondary and Leaf are embedded and aren't listed as separate Catalog cards. |
| 5 | Open the published agent in the Catalog and chat with a prompt that needs a toolkit. | **No toolkits** are shown, and the agent answers without calling any toolkit (unchanged behaviour). |

### Part B: Fork and native toolkits

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | As Forker, open the agent in the Catalog → **Fork** → select **P-Fork**. | The wizard lists Orchestrator, Secondary and Leaf, each with **its own** toolkits under "Tools:". It warns that credentials must be provided manually. |
| 7 | Complete the fork. | The fork succeeds. All 3 agents exist in P-Fork, linked in the same chain. |
| 8 | Open each forked agent's Tools tab. | Every toolkit is **attached** to the agent it belonged to, and to no other agent. Nothing needs to be re-added. |
| 9 | Open P-Fork → Toolkits. | The forked toolkits are listed and Forker can edit them. |
| 10 | Compare Orchestrator's native toolkits with the published version. | Settings are the same. The toolkit with a tool subset has **only those tools** selected. |
| 11 | Open the indexed toolkit. | It uses P-Fork's vector store. No index schedule is set and no index data is copied. |
| 12 | Open the forked Orchestrator's settings. | Internal tools and the step limit match the published agent. |

### Part C: Remote MCP, OpenAPI and local MCP

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Open Secondary's forked remote MCP. | The URL, `X-Client-Name` and the selected tools match. The `Authorization` value is **masked** (`***MASKED***`). |
| 14 | Open Secondary's forked OpenAPI toolkit. | The spec and the 2 selected operations match. The secret header is removed or masked. |
| 15 | Open Leaf's forked local MCP. | It is attached and shows **offline** / not available. |
| 16 | Configure credentials for the native toolkits and enter Forker's own MCP header and OpenAPI secret. | Saved. |
| 17 | Chat with the forked Orchestrator using a task that needs its own native toolkit. | The toolkit is called successfully. The offline local MCP doesn't cause an error. |
| 18 | Chat using a task that needs Secondary's OpenAPI, then its remote MCP. | Orchestrator delegates to Secondary. The OpenAPI operation and the MCP tool are both called successfully. |
| 19 | Chat using a task that needs Leaf's local MCP. | The agent clearly says the tool isn't available. Not an empty reply. |
| 20 | As Forker, add the corresponding local MCP in their environment. Repeat step 19. | The local MCP shows **online**. The chain Orchestrator → Secondary → Leaf calls the local MCP tool successfully. |

### Part D: Snapshot = published version

| # | Action | Expected Result |
|---|--------|-----------------|
| 21 | As Author, in P-Author change a setting on one of Orchestrator's toolkits, remove a toolkit from Leaf and add a new toolkit. Don't publish. Fork the Catalog agent again into a **second** project. | The fork reflects the **published** version: old setting, removed toolkit still present, no new toolkit. |
| 22 | Publish the changed agent as a new version and fork **that** version into a third project. | The fork has the new setting and the new toolkit, and no removed toolkit. |
| 23 | Edit a toolkit in one forked project. | The other forks and the Catalog agent are unchanged. |

### Part E: Security

| # | Action | Expected Result |
|---|--------|-----------------|
| 24 | As the third user, GET the Catalog version details of the published Orchestrator and of the embedded Secondary and Leaf. | `meta.fork_toolkits` is present for each. |
| 25 | Search those responses for the secret values, the sensitive MCP header value and Author's email. | None appear. Each entry has only `type`, `name`, `settings`, `selected_tools`, `meta` and `import_uuid`. There are no index schedules and no `parent_*` lineage keys. |
| 26 | As Forker, **Export** the Catalog agent (not Fork) and open the file. Then GET a forked agent's version. | The export has no toolkits and no `fork_toolkits` key. The forked version's meta has no `fork_toolkits` key either. |
| 27 | **[Cleanup]** Delete the forked agents and toolkits in the target projects and unpublish the test agent. | Cleanup done. |

---

## Expected Final State

Every agent in the fork has its own toolkits, attached as in the published version, and they work once Forker adds their own credentials and local MCP. The Catalog copy still exposes no toolkits and no secrets.

---

## Pass/Fail Criteria

**Pass:**
- Native toolkits, remote MCPs, local MCPs and OpenAPI are carried for the parent and for every sub-agent, on the right agent, with the same settings and selected tools.
- Sensitive values are masked or stripped. Index schedules are not carried.
- The local MCP works after Forker adds the corresponding local MCP. The agent works without it until then.
- The fork reflects the published version, not live source edits.
- The Catalog copy shows and runs no toolkits. Its snapshot, exports and forked meta leak nothing.
- AI validation rule 9 is applied to both the main agent and its sub-agents.

**Fail:**
- Any toolkit is missing, unattached or on the wrong agent, or a sub-agent arrives without its toolkits.
- A secret, unmasked sensitive header, email or schedule is exposed anywhere.
- The agent breaks or returns an empty reply because of the offline local MCP.
- The fork reflects unpublished source changes.
