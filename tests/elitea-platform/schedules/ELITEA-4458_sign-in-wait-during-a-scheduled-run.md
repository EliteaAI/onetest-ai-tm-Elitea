---
id: ELITEA-4458
title: "Schedules — a toolkit sign-in during the run: saved with a notice, waits for the owner, sign in and approve continues, Run without asking fails"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, int:oauth, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4458: Schedules — a toolkit sign-in during the run: saved with a notice, waits for the owner, sign in and approve continues, Run without asking fails

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify #7304 for a toolkit that needs a personal OAuth sign-in: with **Pause and ask me** the schedule can be saved (notice, not a block) and the run waits for the owner, who signs in and approves; reject ends it as Failed. With **Run without asking** the save is blocked and a run never waits.

---

## Preconditions

- A team project **P**; the tester owns the schedules.
- An agent **AG** with a toolkit that needs a **personal sign-in** and has no stored login: a remote MCP server with OAuth, or a SharePoint / OpenAPI delegated credential.
- The tester's browser has no sign-in for that toolkit.
- "Run without asking" is allowed in P (for Part B).

---

## Steps

### Part A: Pause and ask me

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In AG → Schedules, create a schedule with **Pause and ask me**. Click Save. | The review shows a **notice**, not a block: "This agent needs a personal sign-in. The run waits until you sign in and approve." with the hint "Sign in or add the credentials before the run; otherwise the run waits for you." and the link "Open agent to sign in or add credentials". The schedule saves. |
| 2 | Test run. | Status **Waiting for approval**. Run log "Paused for approval: a sign-in is needed for <toolkit>". No URL or token in the log. |
| 3 | Check notifications. | One notice naming the toolkit and that a sign-in is needed. |
| 4 | Open the run. | 'Authorization is required for toolkit "<name>". Authorize now, then approve.' **Approve is disabled.** |
| 5 | Click **Sign in**, complete the sign-in. | Approve becomes enabled. |
| 6 | Approve. | The run continues **from the paused step** (earlier steps not repeated) and ends **Success**. |
| 7 | Clear the browser sign-in, Test run, and **Reject** (skip). | **Failed**, reason "rejected by the owner". |
| 8 | **Record:** with an **expired** stored browser token for the toolkit server, open the waiting run. | Approve may be enabled (known gap: tokens are not checked). Note what happens on Approve. |
| 9 | DevTools on Approve: check the resume request. | **Record** which browser tokens are sent (known gap: all stored tokens, as in chat). |

### Part B: Run without asking

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Change the rule to **Run without asking** and Save. | Save is **blocked** (409) with the sign-in finding. |
| 11 | If a "Run without asking" run still reaches the sign-in (e.g. sign-in revoked after save), check the run. | **Failed** "the toolkit '<name>' needs a sign-in and this schedule does not ask the owner". It never waits. |
| 12 | Switch the rule back and forth in the form before saving. | The sign-in item moves between **notice** (Pause) and **blocking** (Run without asking). |

---

## Expected Final State

The Pause and ask me run finished after the owner signed in; rejected and Run without asking runs ended as Failed with their reasons.

---

## Pass/Fail Criteria

**Pass:**
- Saving and waiting behave per approval rule as above; approve resumes from the paused step.

**Fail:**
- A Pause and ask me run fails with "the run needs a human answer" (the old behaviour).
- A Run without asking run waits.
- The run log or notice contains a URL or a token.
