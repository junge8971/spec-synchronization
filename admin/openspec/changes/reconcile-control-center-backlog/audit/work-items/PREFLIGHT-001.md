# PREFLIGHT-001 — child runtime and browser readiness

- Task: 1.2; status: blocked.
- Authorized retry: temporary user profile with `read, mcp:chrome-devtools/list_pages` failed before launch with unresolved MCP selector. No new run ID. Temporary profile deleted. Receipt: `../readiness-child-retry.md`. No further retry or fallback authorized.
- Owner: collector-preflight (researcher); model: openai-codex/gpt-6-astra, medium.
- Inputs: manifest.json revision 1; current browser connection. No content collection yet.
- Cwd: /home/user/my/work/codesrc/projects/CAM/tsam-admin-front; HEAD bc0d9800f25a90989b9c73c76f91996f8300f1d3.
- Browser lease: exclusive to this child during run; parent and other children do not navigate/read browser.
- Allowed: inspect own available tools, read manifest, call MCP list_pages once; report only presence of target tabs MOS-623, Confluence 238324523, API docs. Do not expose unrelated tab details.
- Forbidden: page navigation, page content collection, external writes, source/planning file edits, credential inspection, other agents, tests.
- Output: runtime-bound audit/readiness-child.md; no other writes.
- Acceptance: exact runtime model/thinking supplied by launch receipt, usable local read tool and successful MCP listing; report missing tools/errors honestly. Does not prove site content access.
- Reviewer: supervisor for infrastructure readiness, not product acceptance.
- Stop: first infrastructure error; no alternate tool protocol/model.
- Checkpoint: run `bf4112c0-5af0-4767-945a-3f082b8b72d1` failed. Receipt: `../readiness-child.md`. Researcher requested unavailable web_search/fetch_content/get_search_content/source_check; child runtime also lacked MCP. Local reads succeeded, browser not accessed. No retry or fallback launched. Task 1.2 remains unchecked. HEAD unchanged; only task 1.1 checkbox differs from planning baseline; new audit files are listed by explicit filesystem inspection because Git ignores them.
