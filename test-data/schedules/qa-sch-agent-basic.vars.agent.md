---
name: QA-SCH Agent basic
description: 'QA test data for schedules (#7011). v base: one short sentence. v vars: {{topic}} / {{team}} placeholders. Safe
  to reuse; do not change.'
version: vars
model: global.openai.gpt-5.6-luna
max_tokens: -1
agent_type: agent
step_limit: 25
variables:
- name: topic
  value: release notes
  id: 1
- name: team
  value: QA
  id: 2
---

Start the answer with the word TWO. Then summarise {{topic}} for the {{team}} team in one sentence.