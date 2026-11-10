---
name: QA-SCH Agent ask user
description: 'QA test data for schedules (#7011): internal tool ask_user on, so every schedule of it is Blocked. Do not change.'
model: global.openai.gpt-5.6-luna
max_tokens: -1
agent_type: agent
step_limit: 25
internal_tools:
- ask_user
---

Before answering, always ask the user what to do.