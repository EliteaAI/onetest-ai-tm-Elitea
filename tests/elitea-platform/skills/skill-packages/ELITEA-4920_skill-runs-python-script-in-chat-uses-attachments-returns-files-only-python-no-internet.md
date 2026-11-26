---
id: ELITEA-4920
title: "Skill runs its Python script in chat, uses attached files and returns created files; only Python runs, without internet"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:chat, feat:attachments, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4920: Skill runs its Python script in chat, uses attached files and returns created files; only Python runs, without internet

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that when a skill's instructions call for one of its Python scripts, the script runs and the answer uses its result; that a file attached to the chat can be used by the script and a file the script creates appears in the chat; and that only Python scripts run, without internet access.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `qa-7185-calc` is imported from the ZIP in Test Data.
- Agent `qa-7185-agent` has `qa-7185-calc` attached.
- `data.csv` from Test Data is saved locally.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill ZIP | `qa-7185-calc.zip`: `SKILL.md`, `rules.md`, `scripts/calc.py`, `scripts/readcsv.py`, `scripts/run.sh`, `scripts/net.py` |
| `scripts/calc.py <a> <b>` | Prints the sum and writes `output/result.txt` |
| `scripts/readcsv.py` | Prints the total of the `amount` column of the CSV files under `inputs/` |
| `scripts/run.sh` | Shell script that prints a marker |
| `scripts/net.py` | Makes an HTTP request to https://example.com and prints the error |
| `data.csv` | `item,amount` with rows `a,10`, `b,20`, `c,12.5` |

`SKILL.md` tells the agent to read `rules.md`, to use `calc.py` and `readcsv.py` as described, and to run `run.sh` and `net.py` only when the user asks for them by name.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **New chat** → **+** → **Agents** → `qa-7185-agent`. Attach `data.csv` and ask for the total of the amount column, then for 2 + 3 | Chips "Attachments: read_multiple_files" and "Skill: qa-7185-calc · Nms" appear. The answer gives the total 42.5 and 2 + 3 = 5 |
| 2 | Check under the answer | The file created by the script appears as a `result.txt` chip and can be opened or downloaded |
| 3 | Ask to run `scripts/run.sh` by name | The script is not run. The answer says only `.py` scripts run |
| 4 | Ask to run `scripts/net.py` by name and report what it printed | The script runs but the request fails (for example `Network blocked … URLError`). The chat replies and does not hang |

---

## Expected Final State

The chat shows the script results and the `result.txt` file. Delete the chat, the agent and the skill after the run.

---

## Pass/Fail Criteria

**Pass:**
- Python scripts run, use the attached file and return the created file.
- `.sh` scripts and network access are blocked.

**Fail:**
- The script does not run, or the answer does not use its result.
- The attached file is not available to the script, or the created file is not shown.
- `run.sh` runs, or the network request succeeds.

---

## Notes

- The **Test Agent** panel has attachments disabled; use a regular chat for step 1.
- The skill instructions shown in the "Skill: …" chip say that scripts run offline in a sandbox, attachments appear under `inputs/`, files written under `output/` are shared with the user, and only `.py` files run.
