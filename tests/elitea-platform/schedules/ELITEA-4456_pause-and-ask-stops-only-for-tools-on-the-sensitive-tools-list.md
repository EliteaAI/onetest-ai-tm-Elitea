---
id: ELITEA-4456
title: "Schedules — \"Pause and ask me\" stops only for tools on the Sensitive Tools list, matched by spelling, toolkit name and tool selection"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:guardrails, issue:7314, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7314", "EliteaAI/elitea_issues#7304"]
---

# ELITEA-4456: Schedules — "Pause and ask me" stops only for tools on the Sensitive Tools list, matched by spelling, toolkit name and tool selection

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify #7314 (which overrides #7304): a scheduled run with **Pause and ask me** pauses only before a tool on the global **Sensitive Action Tools** list. Other tools run without stopping. The list entry is matched like the runtime guard: case and separators are ignored, an alias prefix (`x___tool`, `x:tool`) is ignored, and the key may be the toolkit type or the toolkit name. The risk review at save time shows the same tools.

Chat (not scheduled) sensitive-tool approval is covered by `sensitive-tool-calling` (e.g. ELITEA-1004, ELITEA-1015).

---

## Preconditions

- **Test data:** import [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- Admin Portal access (platform admin): Configuration → **Guardrails** → **Sensitive Action Tools**.
- A team project **P**; the tester is the schedule owner.
- An agent **AG** with a **GitHub** toolkit **GH** ("My GitHub") on a test repository. AG's instructions make it call `get_issue` for prompt A and `create_pull_request` for prompt B.
- A second GitHub toolkit **GH2** with another name, for step 9.

---

## Test Data

| Item | Value |
|------|-------|
| Base list | `{"github": ["create_pull_request"]}` |
| Prompt A (non-sensitive) | "Read issue #1 and summarise it" |
| Prompt B (sensitive) | "Open a pull request from branch `test` to `main` titled 'Schedule test'" |
| Prompt C (mixed) | "Read issue #1, then open a pull request …" |

---

## Steps

### Part A: listed vs not listed

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the base list. In AG → Schedules, create a schedule with prompt A, approval rule **Pause and ask me**. | The risk review shows no sensitive item for `get_issue`. Saved. |
| 2 | **Test run** the schedule. | The run ends **Success**. Run log has no `paused` line. No approval notice. |
| 3 | Change the prompt to B, save. | The risk review lists 'Tool "create_pull_request" of toolkit "My GitHub" needs approval' (with its badge / effect). |
| 4 | Test run. | Status **Waiting for approval** before the tool runs. Run log "Paused for approval: My GitHub · create_pull_request". One "needs approval" notice. |
| 5 | Reject the run (see ELITEA-4457 for approve). Change the prompt to C, Test run. | `get_issue` runs; the run pauses only at `create_pull_request`. |
| 6 | Remove `create_pull_request` from the list. Test run prompt B. | No pause; the run continues (Success or the tool's own result). |

### Part B: spelling and key variants (set one at a time, then Test run prompt B)

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | List `{"github": ["Create-Pull-Request"]}`, then `["CreatePullRequest"]`. | Each: the review lists the tool and the run pauses. |
| 8 | List `{"github": ["github___create_pull_request"]}`, then `["github:create_pull_request"]`. | Each: matched, the run pauses. |
| 9 | List `{"My GitHub": ["create_pull_request"]}` (toolkit **name** as key). Run with GH, then attach GH2 instead and run. | GH: pauses. GH2: does not pause (the key names only "My GitHub"). |

### Part C: which toolkit tools are scanned

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Base list. In AG, GH's **Tools**: tick a subset **with** `create_pull_request`. Save the schedule. | Review: 'Tool "create_pull_request" of toolkit "My GitHub" needs approval'. |
| 11 | Tick a subset **without** `create_pull_request` (e.g. only `get_issue`). Save the schedule. | No sensitive item. A run never pauses. |
| 12 | Untick all (= **all tools**). Save the schedule. | The review still lists `create_pull_request`, taken from the Sensitive Tools list. A run with prompt B pauses. |
| 13 | Agent with a toolkit that uses a **personal credential** and no listed tool. Save, then run. | The personal-credential confirm is shown at save. The run log risk check says "Risk check: OK" and the run does not pause. |

---

## Expected Final State

Only tools on the Sensitive Tools list paused the runs; every other tool ran without stopping.

---

## Pass/Fail Criteria

**Pass:**
- Non-listed tools never pause a "Pause and ask me" run.
- Every listed spelling and the toolkit-name key are matched, at save and at run time.
- The tool selection rules in Part C hold.

**Fail:**
- A non-listed tool pauses the run (the #7314 bug).
- A listed tool runs without a pause, or the review and the run disagree.
