---
id: ELITEA-5007
title: "Published agent in the Catalog does not show or run its attached pipelines"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5007: Published agent in the Catalog does not show or run its attached pipelines

**Module:** agents-publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the pipelines carried for forking are not visible on the published agent and are not used when the published agent runs in chat, while embedded sub-agents keep working.

---

## Preconditions

- The #7062 fix is deployed.
- In P-Author: agent **A** with pipeline **P1** (with an agent node calling **A1** and a nested pipeline **P2**) and a plain sub-agent **B**, published after the deploy.
- P1 does something that only it can answer, e.g. a code node that returns the fixed text `PIPELINE-7062-MARKER`.
- A user **Viewer** who is not a member of P-Author.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline marker | `PIPELINE-7062-MARKER` |
| Prompt 1 | "Run the pipeline and return its output." |
| Prompt 2 | A task that only sub-agent B can do. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Viewer, open A in the Catalog. Check the details and toolkits section. | No pipeline, no nested agent and no toolkit is shown. |
| 2 | Search the Catalog for `P1`, `P2` and `A1`. | None of them is listed as a separate Catalog card. |
| 3 | Start a chat with the published A and send prompt 1. | The answer does **not** contain `PIPELINE-7062-MARKER`. No pipeline run appears in the thinking steps. |
| 4 | Send prompt 2. | A delegates to the embedded sub-agent B and gets an answer (no regression). |
| 5 | **[Cleanup]** Unpublish A. | Cleanup done. |

---

## Expected Final State

The Catalog copy behaves as before: no pipeline is shown or run, and embedded sub-agents still work.

---

## Pass/Fail Criteria

**Pass:**
- The pipeline tree is not shown and not run on the published agent.
- Embedded sub-agents still work in chat.

**Fail:**
- Any pipeline, nested agent or toolkit is shown or run on the published agent, or listed in the Catalog.
