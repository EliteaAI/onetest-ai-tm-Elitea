# Test data: chat runs continue in the background (#7385)

Fixtures for the cases in `tests/elitea-platform/chat-interface/chat-runs-continue-in-background/` (ELITEA-4930 to ELITEA-4952). Recreated per environment from the files below. No secrets: both toolkits call public, no-auth APIs.

These files live outside `tests/` on purpose: the index builder reads every `.md` under `tests/` as a test case.

## Toolkits

Create two OpenAPI toolkits from the specs (no credentials):

| File | Toolkit | Tools | Why |
|---|---|---|---|
| `postman-echo-delay.openapi.yaml` | Postman Echo delay | `waitSeconds` (`GET https://postman-echo.com/delay/{seconds}`, 0–10 s) | A deterministic wait, so a run lasts long enough to leave and come back |
| `jsonplaceholder.openapi.yaml` | JSONPlaceholder | `getPost`, `getUser` | Fixed data with a known answer (post 2 / post 3 authors) |

## Agents and pipeline

| File | Entity | Settings | What it does | Used by |
|---|---|---|---|---|
| `r7385-longrunner.instructions.md` | Agent **R7385LongRunner** | Both toolkits, reasoning low, default step limit | About 45 s, 5 tool calls (3 × `waitSeconds` 10, `getPost`, `getUser`); answers `RUN-DONE <word>` | Most cases |
| `r7385-askuser.instructions.md` | Agent **R7385AskUser** | Both toolkits, internal tool **Ask User** on | Waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2); answers `ASK-DONE post <id>` | ELITEA-4932, 4946, 4952 |
| `r7385-failer.instructions.md` | Agent **R7385Failer** | Both toolkits, **step limit 3** | Needs 6 tool steps, so the run fails with "Maximum tool execution iterations (3) reached." | ELITEA-4948 |
| `r7385-pipe.pipeline.yaml` | Pipeline **R7385Pipe** | Postman Echo delay toolkit; replace `<Postman Echo delay toolkit name>` with your toolkit's name | `waitSeconds` 10 → LLM → `waitSeconds` 10 → LLM; answers `PIPE-DONE <word>` | ELITEA-4939 |

## Conversations

Each case names the conversations it needs (for example **A** with R7385LongRunner as the participant, and an idle **B** to switch to). Clear a conversation's messages before reusing it. Otherwise the agent may reuse earlier results and skip its tools.

## Regression cases (ELITEA-4953 to ELITEA-4957)

These cases are stateless. Each one creates its own toolkits, agent and conversations in its **Setup** section from the files above, with a per-run name suffix (`autotest_echo_<sfx>`, `autotest_jph_<sfx>`, `autotest_runner_<sfx>` or `autotest_askuser_<sfx>`, `autotest_run_A_<sfx>`, …), and deletes them in its **Teardown** section, also when the test fails. They never use the persistent fixtures described above.

## Tips

- Plain chats (ELITEA-4938): if the project's default model loads skills that cap the answer format, pick another model in the composer.
- The New response dot is held in the browser only. Come back to the chat list in-app, not with a page reload.
- To stop a run through the API, take the run uuid from the latest `chat_run_status` "running" socket frame of that chat.
