# Agent Quota Management Rules

To conserve the LLM context window and token quota, all agents MUST adhere to these strict constraints:

## 1. File Size Limits & Modularity
- **Never read monolithic files:** If a file is large, do NOT use `view_file` indiscriminately. Use `view_file_outline` or `grep_search` to target specific functions.
- **Enforce the Manager Pattern:** Keep all logic highly modularized (e.g., `SovereignManager`). Strive to keep individual files under 300 lines of code.

## 2. Iteration Caps (Death Loops)
- **The "3-Fail" Rule:** If a unit test fails or a bug persists after 3 automated attempts to fix it, you MUST stop iterating immediately. Do not burn quota guessing.
- **Fail Logs:** Output the error context to the user so they can intervene logically.
- **Stack Traces:** When reading terminal error logs, avoid dumping massive stack traces into memory. Focus on the specific Exception at the bottom of the log.

## 3. Context Hygiene
- Do not summarize large swathes of code repeatedly. Use specific line numbers and file names when discussing changes.
- **New Sessions:** If an architectural design phase or a complex bughunt goes on for an extended period, it's safer to summarize the findings, close the active session, and start a fresh chat to reset the context window cost.
