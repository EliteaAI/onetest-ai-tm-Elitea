# Test data: chat runs continue in the background (#7385)

Test data for the cases in `tests/elitea-platform/chat-interface/chat-runs-continue-in-background/` (ELITEA-4930 to ELITEA-4952) and their regression cases (ELITEA-4953 to ELITEA-4957). No secrets: both toolkits call public, no-auth APIs.

These files live outside `tests/` on purpose: the index builder reads every `.md` under `tests/` as a test case.

## Toolkit specs

OpenAPI specs (no credentials):

| File | Toolkit | Tools | Why |
|---|---|---|---|
| `postman-echo-delay.openapi.yaml` | Postman Echo delay | `waitSeconds` (`GET https://postman-echo.com/delay/{seconds}`, 0–10 s) | A deterministic wait, so a run lasts long enough to leave and come back |
| `jsonplaceholder.openapi.yaml` | JSONPlaceholder | `getPost`, `getUser` | Fixed data with a known answer (post 2 / post 3 authors) |

## Import files (manual cases)

Import from the Agents page (**Add agent** → **Import from file**) or the Pipelines page (**Add pipeline** → **Import from file**). The import creates the toolkits `r7385_echo` (Postman Echo delay) and `r7385_jph` (JSONPlaceholder) or reuses them if they already exist. The "toolkits need additional configuration" notice can be ignored.

| File | Creates | What it does | Used by |
|---|---|---|---|
| `r7385-longrunner.agent.md` | Agent **R7385LongRunner** | About 45 s, 5 tool calls (3 × `waitSeconds` 10, `getPost`, `getUser`); answers `RUN-DONE <word>` | Most cases |
| `r7385-askuser.agent.md` | Agent **R7385AskUser** (Ask User on) | Waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2); answers `ASK-DONE post <id>` | ELITEA-4932, 4946, 4952 |
| `r7385-failer.agent.md` | Agent **R7385Failer** (step limit 3) | Needs 6 tool steps, so the run fails with "Maximum tool execution iterations (3) reached." | ELITEA-4948 |
| `r7385-pipe.pipeline.md` | Pipeline **R7385Pipe** | `waitSeconds` 10 → LLM → `waitSeconds` 10 → LLM; answers `PIPE-DONE <word>` | ELITEA-4939 |

Each case creates its agents and conversations new, and deletes them, with the toolkits, in its **Teardown**. Don't reuse a conversation from an earlier run: the agent may reuse earlier results and skip its tools.

The `.instructions.md`, `.pipeline.yaml` and `.openapi.yaml` files hold the same agents and toolkits in parts. The regression cases use them.

## Regression cases (ELITEA-4953 to ELITEA-4957)

These cases are stateless. Each one creates its own toolkits, agent and conversations in its **Setup** section from the files above, with a per-run name suffix (`autotest_echo_<sfx>`, `autotest_jph_<sfx>`, `autotest_runner_<sfx>` or `autotest_askuser_<sfx>`, `autotest_run_A_<sfx>`, …), and deletes them in its **Teardown** section, also when the test fails.

## Tips

- Plain chats (ELITEA-4938): if the project's default model loads skills that cap the answer format, pick another model in the composer.
- The New response dot is held in the browser only. Come back to the chat list in-app, not with a page reload.
- To stop a run through the API, take the run uuid from the latest `chat_run_status` "running" socket frame of that chat.
