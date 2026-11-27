---
id: ELITEA-5010
title: "AI publish validation rule 9 says pipelines and toolkits are not available on the published agent, not that they are dropped"
priority: low
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, feat:ai-validation, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5010: AI publish validation rule 9 says pipelines and toolkits are not available on the published agent, not that they are dropped

**Module:** agents-publishing · **Priority:** Low · **Type:** Functional

**Objective:** Verify that the rule 9 "Toolkit Dependencies" warning no longer claims pipelines and toolkits "will not be included" after publishing, since forks now include them.

**Note:** The LLM writes the warning text, so the wording varies between runs. Check the meaning, not the exact words.

---

## Preconditions

- The #7062 fix is deployed. AI publish validation is enabled.
- In P-Author: agent **A** with pipeline **P1** and toolkit **T1** attached.

---

## Test Data

| Field | Value |
|-------|-------|
| Instructions without fallback | "Always run the pipeline and use the toolkit to look up the item before answering." |
| Fallback text | "If the pipeline or toolkit is not available, explain what is needed and answer from general knowledge." |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Put the no-fallback instructions on A. Start publishing and run the AI validation. | A rule 9 "Toolkit Dependencies" **warning** is shown on `instructions`. |
| 2 | Read the warning text. | It says the pipeline/toolkit is **not available on the published agent** (or similar). It does **not** say they "will not be included", are "dropped" or are "lost". |
| 3 | Run the validation 2 more times. | The meaning stays the same in every run. |
| 4 | Add the fallback text and validate again. | No Toolkit Dependencies warning. |
| 5 | **[Cleanup]** Cancel the publish or unpublish. | Cleanup done. |

---

## Pass/Fail Criteria

**Pass:**
- The warning describes the dependency as not available on the published agent.
- No warning when a fallback is given.

**Fail:**
- The warning says pipelines or toolkits will not be included, or are dropped or lost.
