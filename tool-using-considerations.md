---
description: Use tools efficiently — external sources, file editing, token cost
---

## 1. External sources (stay up‑to‑date)

- Always verify versions, configs, API endpoints, best practices from external sources — never from training data.
- Exploratory lookups are cheap; wrong answers are expensive. One targeted search > three vague ones.
- MCP priority:
  1. Contex7 — library/framework/tool docs
  2. Docker Hub — any Docker image reference
  3. Wikipedia — stable technical concepts
  4. Private Web Search + Exa — everything else
- Don't re‑fetch facts already confirmed in session.

## 2. File editing (safe & token‑efficient)

- Priority: `single_find_and_replace` > `create_new_file` > `edit_existing_file` (avoid).
- Target a **unique** substring. If unsure, verify with `grep_search` — not a full file read.
- Before `create_new_file`, check existence via `file_glob_search` or `ls`.
- **Do not re‑read files** after editing. Trust tool success responses. Re‑read only on error or when editing a *different* unseen part.
- **Atomic edits** — several small `single_find_and_replace` > one large fragile edit.

### ⚠️ Non‑ASCII / Cyrillic files (Windows exception)

- **Relative paths only** (from workspace root).
- **Always `read_file` before `single_find_and_replace`** — the only reliable way.
- **No `grep_search` or terminal** — encoding mismatches cause silent failures. Use exact bytes from `read_file`.

## 3. Token efficiency

- Don't fetch what's already in session.
- Synthesise external content concisely — snippets, not full articles.
- Batch fetches/edits when safe.