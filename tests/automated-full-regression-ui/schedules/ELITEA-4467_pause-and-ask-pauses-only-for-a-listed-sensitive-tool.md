---
id: ELITEA-4467
title: "Schedules — Pause and Ask Me Pauses Only for a Listed Sensitive Tool; Approve Continues and Reject Fails"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:schedules, feat:guardrails, issue:7314, issue:7304, r-2.0.8, issue:7432]
requirements: ["EliteaAI/elitea_issues#7314", "EliteaAI/elitea_issues#7304", "EliteaAI/elitea_issues#7432"]
---

# ELITEA-4467: Schedules — Pause and Ask Me Pauses Only for a Listed Sensitive Tool; Approve Continues and Reject Fails

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of #7314 on top of #7304, using the built-in Artifact toolkit (no external account): a non-listed tool runs without a pause; a listed tool pauses; approve continues; reject fails. Manual source: ELITEA-4456, ELITEA-4457.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md), [`qa-sch-agent-artifact.non-sensitive.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.non-sensitive.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- Sensitive Action Tools (Admin Portal → Configuration → Guardrails) contains `{"artifact": ["create_file"]}` and no other Artifact tool.
- An agent with an Artifact toolkit; instructions: prompt A lists the bucket's files, prompt B creates a file.
- Two "Pause and ask me" schedules: SA with prompt A, SB with prompt B.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Test run SA. | Ends **Success**; the run log has no `paused` line. |
| 2 | Open SB's Save review. | Lists 'Tool "create_file" of toolkit "<name>" needs approval'. |
| 3 | Test run SB. | Status **Waiting for approval**; the run log has "Paused for approval: <toolkit> · create_file"; the runs panel shows "Action needed: this run is waiting for you". |
| 4 | Check the pause text. | No "(+N more)" for a single tool (known bug #7432: shows "(+1 more)"). |
| 5 | Open the run's chat and approve. | The file is created; the run ends **Success**. |
| 6 | Test run SB again and reject. | **Failed** "rejected by the owner"; no new file. |

---

## Expected Final State

One file created; two runs Success, one Failed.

## Teardown

Delete the created file, the schedules and the agent.
