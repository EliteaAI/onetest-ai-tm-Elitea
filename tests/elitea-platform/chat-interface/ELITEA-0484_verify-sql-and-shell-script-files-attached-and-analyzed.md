---
id: ELITEA-0484
title: "Verify SQL and Shell Script Files Attached and Analyzed"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, story:3671, r-2.0.1, shell, sql]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0484: Verify SQL and Shell Script Files Attached and Analyzed

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that SQL and Shell script files (.sql, .sh), which are commonly used by DevOps and data engineering users, can be attached and analyzed. These are distinct from typical programming languages in that they are often used for database queries and automation scripts.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open with a capable LLM
3. Backend returns `.sql` and `.sh` in `code_types` for the project
4. Test files available: `query.sql` and `deploy.sh`

## Test Data

- `query.sql`: A SQL file with a SELECT query involving JOINs and a potential N+1 query pattern (~500 bytes)
- `deploy.sh`: A shell script with deployment commands and a potential security issue (e.g., storing a password in plain text) (~500 bytes)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Conversation is displayed |
| 2 | Click attachment button and select `query.sql` | `query.sql` attaches. No error. |
| 3 | Type: "Review this SQL query for performance issues" and send | Message and SQL file sent; AI processes |
| 4 | Verify AI responds with SQL-specific feedback referencing the query content | AI mentions the query, potential performance issues, or references SQL-specific elements from the file |
| 5 | Clear attachments (if necessary) and click attachment button; select `deploy.sh` | `deploy.sh` attaches. No error. |
| 6 | Type: "Review this shell script for security issues" and send | Message and shell script sent; AI processes |
| 7 | Verify AI responds with shell script-specific feedback | AI references the script content, mentions the hardcoded password or other security concern |

## Expected Final State

AI references the script content, mentions the hardcoded password or other security concern

## Pass/Fail Criteria

- PASS: Both `.sql` and `.sh` files attach without error; AI responses reference specific content from each file type
- FAIL: Either file type is rejected; AI cannot read file content; error during attachment or send
