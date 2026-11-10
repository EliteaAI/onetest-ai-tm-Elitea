# Test data: Schedules (scheduled agents and pipelines, #7011)

Agents and pipelines used by the Schedules test cases (`tests/elitea-platform/schedules/`, `tests/automated-full-regression-ui/schedules/`). Exported from ELITEA (NEXT, 2026-11-10) as Markdown. No secrets: the files hold names, instructions, models and toolkit settings only.

These files live outside `tests/` on purpose: the index builder reads every `.md` under `tests/` as a test case.

## Files

| File | Entity | What it is | Used by |
|---|---|---|---|
| `qa-sch-agent-basic.agent.md` | QA-SCH Agent basic | Plain agent, no tools: "Answer … Start the answer with the word ONE." | Run Now / Test Run, form, editor cards, pause / resume, Run History (ELITEA-4479 to 4484, 4489 to 4491) |
| `qa-sch-agent-artifact.agent.md` | QA-SCH Agent Artifact | Artifact toolkit `qa-sch-artifact` (bucket `qa-sch`) with all 10 tools; "never ask, call the tools the user names" | Sensitive-tool pause, approve / reject, overlap / Skipped (#7435), expiry, "(+1 more)" (#7432) (ELITEA-4456, 4457, 4460, 4467, 4485) |
| `qa-sch-agent-ask-user.agent.md` | QA-SCH Agent ask user | Internal tool `ask_user` on | Blocked "The agent can ask the user a question" (ELITEA-4462) |
| `qa-sch-pipeline-basic.pipeline.md` | QA-SCH Pipeline basic | LLM 1 → Artifact `create_file` → Artifact `delete_file` (toolkit `qa-sch-pipeline-artifact`, file `qa-sch-pipeline.txt`) | Entry point / Prompt run mode (set on the schedule), pipeline pause before `delete_file`; an approved run deletes its own file (ELITEA-4457, 4463, 4480) |
| `qa-sch-pipeline-human-steps.pipeline.md` | QA-SCH Pipeline human steps | HITL node "Review" (approve → LLM 1, reject → END) | Blocked 'Node "Review" waits for a person' (ELITEA-4462, 4468) |
| `qa-sch-agent-basic.vars.agent.md` | QA-SCH Agent basic, version **vars** | "Start with TWO … summarise {{topic}} for the {{team}} team"; variables `topic` = release notes, `team` = QA | `{{variables}}` fields (ELITEA-4480 step 3) |
| `qa-sch-agent-artifact.subset.agent.md` | QA-SCH Agent Artifact, version **subset** | Artifact toolkit `qa-sch-artifact-subset` with only `create_file`, `append_data` | Tool selection: a subset with / without a listed tool (ELITEA-4456 Part C) |
| `qa-sch-agent-artifact.non-sensitive.agent.md` | QA-SCH Agent Artifact, version **non-sensitive** | Artifact toolkit `qa-sch-artifact-safe` with only `append_data`, `create_new_bucket` | "Non-listed tools never pause" (ELITEA-4456 Part A, 4467) |

## Import

ELITEA → **Agents** (or **Pipelines**) → **Import** → pick the file → **Import**. Or via API: the import wizard `POST /api/v2/elitea_core/import_wizard/prompt_lib/{project_id}` (see `elitea-testing/automation/api/client.py` `import_agent` / `import_pipeline`).

## Versions

An export holds **one version** per file, and the import wizard creates **one agent per file** (with that file's `version:` as its only version). So the three `*.<version>.agent.md` files import as **separate agents** with the same name, not as extra versions of one agent.

- For most cases that is enough: import the file of the version the case needs (e.g. `qa-sch-agent-artifact.non-sensitive.agent.md` for "non-listed tools never pause").
- Cases that need **two versions on one agent** (Version dropdown and Version filter, deleting a version: ELITEA-4480, 4483, 4488) need the second version added to the same agent:

| Entity | Add to the same agent | How |
|---|---|---|
| QA-SCH Agent basic | Version **vars** | Agent → New version; copy the instructions and variables from `qa-sch-agent-basic.vars.agent.md` |
| QA-SCH Pipeline human steps | Version **printer** (no export yet) | New version; one Printer node (text "Printed by the QA schedule test.") → END |
| QA-SCH Pipeline human steps | Version **parallel** (optional, no export) | A parallel step whose branch calls Artifact `create_file` (ELITEA-4463 step 2) |

By API (internal ELITEA MCP `…/app/{project}/mcp/elitea_core/applications`): `post_elitea_core_versions` with `application_id`, `name`, `instructions`, `llm_settings`, `variables`, and inline `tools` for a toolkit.

Not exported (create per test): **schedules** (through the Schedules page or `POST /api/v2/elitea_core/schedules/prompt_lib/{project_id}`), a GitHub agent with a credential (ELITEA-4459, 4486).

## Environment setup (per environment)

- **Model:** the files use `global.openai.gpt-5.6-luna`. If it is not available, pick a working model after import.
- **Sensitive Action Tools** (Admin Portal → Configuration → Guardrails): the pause cases expect `artifact: [create_file, delete_file, list_indexes]`. NEXT lists only `delete_file` (2026-11-10): the Artifact agent then pauses only for `delete_file`, and Pipeline basic pauses before **Delete file**.
- **Run without approval** (project Settings → General): on, for the "Run without asking" cases.
- **Schedules Approval Wait Hours** (Admin Portal → Runtime): 24 by default; 1 makes expiry testable.

## Cleanup

Keep the imported entities (shared test data). After a test, delete its schedules (prefix `QA-SCH-`), reject waiting runs, and delete leftover files in bucket `qa-sch` (a rejected Pipeline basic run leaves `qa-sch-pipeline.txt`).

Note: the description of Pipeline basic still says "LLM node then Artifact create_file node"; it now also has the `delete_file` node.
