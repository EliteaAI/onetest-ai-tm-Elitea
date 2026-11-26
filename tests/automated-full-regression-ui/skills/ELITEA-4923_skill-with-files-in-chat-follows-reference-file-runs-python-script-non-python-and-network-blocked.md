---
id: ELITEA-4923
title: "Skill with files in chat: follows its reference file, runs its Python script on an attached file and returns the created file; non-Python and network blocked"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:chat, feat:attachments, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4923: Skill with files in chat: follows its reference file, runs its Python script on an attached file and returns the created file; non-Python and network blocked

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify that in a chat a skill uses its reference file, runs its Python script on a file the user attached, returns the file the script creates, and that only Python runs, without internet access.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `regression-calc-skill` is imported from the ZIP in Test Data and shows **Files – 5**.
- Agent `regression-skill-agent` has the skill attached ("1/50 skills added.").
- `data.csv` from Test Data is saved locally.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill ZIP | `regression-calc-skill.zip`: `SKILL.md`, `rules.md`, `scripts/calc.py`, `scripts/readcsv.py`, `scripts/run.sh`, `scripts/net.py` |
| `rules.md` | "End every answer with `-- CALC-SKILL RULES APPLIED --`" |
| `scripts/calc.py <a> <b>` | Prints the sum and writes `output/result.txt` |
| `scripts/readcsv.py` | Prints the total of the `amount` column of the CSV files under `inputs/` |
| `scripts/net.py` | Makes an HTTP request to https://example.com and prints the error |
| `data.csv` | `item,amount` with rows `a,10`, `b,20`, `c,12.5` |

`SKILL.md` says: "Before answering, read `rules.md` and follow every rule in it." It describes `calc.py` and `readcsv.py`, and says to run `run.sh` and `net.py` only when the user asks for them by name.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **New chat** → **+** → **Agents** → `regression-skill-agent` | The agent is added to the chat |
| 2 | Attach `data.csv` and send "Use regression-calc-skill: give the total of the amount column of the attached CSV, then add 2 and 3" | Chips "Attachments: read_multiple_files" and "Skill: regression-calc-skill · Nms" appear. The answer contains 42.5 and 5 and ends with `-- CALC-SKILL RULES APPLIED --` |
| 3 | Check under the answer | A `result.txt` chip is shown and can be opened or downloaded |
| 4 | Click a "Skill: regression-calc-skill" chip | The OUTPUT panel shows the skill instructions and the `<skill_files>` list |
| 5 | Send "Using regression-calc-skill, run scripts/run.sh by name" | The answer says the script was not run because only `.py` scripts run |
| 6 | Send "Using regression-calc-skill, run scripts/net.py by name and report what it printed" | The answer reports a failed network call (for example `URLError`). The chat does not hang |

---

## Expected Final State

The chat shows three answers that reflect the skill files. Delete the chat, the agent and the skill after the run.

---

## Pass/Fail Criteria

**Pass:**
- The rule from `rules.md` is applied.
- The CSV is read and `result.txt` is returned.
- `.sh` scripts and network access are blocked.

**Fail:**
- The answer ignores `rules.md`.
- There is no script result or no output file.
- `run.sh` executes, or the network call succeeds.

---

## Notes

**Source functional tests:** ELITEA-4919 (step 1, chip panel), ELITEA-4920 (steps 1–4) — AC4–AC5 of EliteaAI/elitea_issues#7185
**Regression rationale:** The new skill runtime (file reads and sandboxed scripts) is the highest-risk part of #7185.
**Selected checkpoints:** reference-file rule; script result; attachment as input; output-file chip; `.sh` blocked; network blocked.
**Not covered:** the `~` mention path (ELITEA-4919 step 3).
- Check numbers and markers, not the exact wording of LLM answers.
- The **Test Agent** panel has attachments disabled; use a regular chat.
