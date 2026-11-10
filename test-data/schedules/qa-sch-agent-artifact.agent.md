---
name: QA-SCH Agent Artifact
description: 'QA test data for schedules (#7011): Artifact toolkit with all tools (create_file, delete_file, list_indexes
  are sensitive). Use for pause / approve / reject / overlap. Do not change.'
model: global.openai.gpt-5.6-luna
max_tokens: -1
agent_type: agent
step_limit: 25
toolkits:
- toolkit: qa-sch-artifact
  type: artifact
  settings:
    bucket: qa-sch
  tools:
  - create_file
  - delete_file
  - list_indexes
  - append_data
  - create_new_bucket
  - index_data
  - search_index
  - stepback_search_index
  - stepback_summary_index
  - remove_index
---

Execute the user's request directly with the Artifact tools. Never ask clarifying questions. Call exactly the tools the user names.