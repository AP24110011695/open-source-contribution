# Open Source Contributions — Ayush (AP24110011695)

One link with everything I ship to open source. Every pull request, bug report and fix below is real, linked, and verifiable — no screenshots-only portfolio.

**About me:** B.Tech CSE student. Python / C++ / React / FastAPI. I contribute to projects in the AI-agents, MCP, developer-tools and web-framework space — picking real bugs, writing failing regression tests first, and seeing fixes through review.

**Snapshot:** 21 open pull requests across 6 projects · 7 bug reports filed · fixes passing CI and reviewed by maintainers · merges tracked here as they land.

---

## How I work

- **Failing regression test first** — prove the bug on the project's own `main`, then show the same test passing with the fix.
- **Read the contribution rules before committing** — DCO sign-offs, PR templates, issue gates; nothing opened that violates a project's flow.
- **Every PR links its issue** (`Fixes #…`), states the root cause, and documents which tests fail on `main`.
- **Reviewer feedback is fixed the same session**, with a short "addressed in `<sha>`" reply on the thread.
- **External services are mocked in tests — never the code under test.**

### Review track record

Across every review bots and maintainers have left on these PRs: **16 findings raised → 14 fixed the same session with regression tests, 1 escalated to a tracked design question for maintainers, 1 documentation wording fix.** Nothing unresolved. Zero findings survived a second review.

Words from project reviewers:

> "This is exactly the fix the docs needed. … No changes needed."
> "Nice catch, and a clean fix."
> "Clean, well-diagnosed fix… exactly right."
> "Excellent root-cause work."
> "Clean, well-evidenced fix… looks ready once the build check finishes."
> — [@rahmanaisha](https://github.com/rahmanaisha), layer5 maintainer, on five of the pull requests below

---

## Phase 1 — First contributions across four projects

The plan: learn four different contribution cultures end to end — an AI agent framework, an MCP server framework, a cloud-native UI project, and an agent-memory library.

### crewAI — AI agent framework

| Pull request | What it fixes | Status |
|---|---|---|
| [#8845 — store sqlite checkpoint data as plain text](https://github.com/crewAIInc/crewAI/pull/8845) | Checkpoint writes crash on SQLite < 3.45 (`no such function: jsonb`) — fixes [#8843](https://github.com/crewAIInc/crewAI/issues/8843) | Open · CI green · in review |
| [#8848 — publish JSON checkpoints atomically](https://github.com/crewAIInc/crewAI/pull/8848) | Interrupted writes left truncated/corrupt checkpoint files — fixes [#8846](https://github.com/crewAIInc/crewAI/issues/8846) | Open · CI green · in review |
| [#8849 — tolerate malformed tool-call arguments in history replay](https://github.com/crewAIInc/crewAI/pull/8849) | Uncaught `JSONDecodeError` crash replaying Anthropic/Bedrock conversations — fixes [#8847](https://github.com/crewAIInc/crewAI/issues/8847) | Open · CI green · in review |

All three bugs were found by code inspection (the issues are mine too), with security review from the project's bot reporting no findings.

### fastmcp — MCP server framework

| Pull request | What it fixes | Status |
|---|---|---|
| [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) | JSON-pointer-escaped schema names broke schema extraction — fixes [#6034](https://github.com/PrefectHQ/fastmcp/issues/6034) | Open · awaiting maintainer issue assignment |
| [#6185 — keep `tools/list` working when a root `$ref` resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | Whole-server tools listing crashed on valid schemas — fixes [#6125](https://github.com/PrefectHQ/fastmcp/issues/6125) | Open · awaiting maintainer issue assignment |
| [#6187 — support non-identifier variables in URI templates](https://github.com/PrefectHQ/fastmcp/pull/6187) | `{$top}`-style template variables never matched or forwarded | Open · in review after triage fixes |
| [#6188 — keep result hydration faithful for union coercions](https://github.com/PrefectHQ/fastmcp/pull/6188) | `0 → False`-style coercions silently replaced typed results | Open · in review after triage fixes |
| [#6189 — normalize CR/CRLF in generate-cli descriptions](https://github.com/PrefectHQ/fastmcp/pull/6189) | Windows line endings produced `SyntaxError` in generated CLIs | Open · awaiting maintainer issue assignment |

1,400+ existing tests pass on each; the triage-reviewer bot's findings on two of these were fixed the same day.

### layer5 — cloud-native UI

| Pull request | What it fixes | Status |
|---|---|---|
| [#8277 — case-study banner fits its container on mobile](https://github.com/layer5io/layer5/pull/8277) | Logo/graphic overflowed on small viewports — fixes [#8272](https://github.com/layer5io/layer5/issues/8272) | Reviewed "no changes needed" · awaiting merge |
| [#8278 — pricing cards reference real tier names](https://github.com/layer5io/layer5/pull/8278) | Bylines named tiers that don't exist ("Free", "Team") — fixes [#8258](https://github.com/layer5io/layer5/issues/8258) | Reviewed "no changes needed" · awaiting merge |
| [#8279 — Sistent icons docs: valid imports, preview matches snippet](https://github.com/layer5io/layer5/pull/8279) | Docs snippet imported non-existent exports; preview didn't match the code — fixes [#8257](https://github.com/layer5io/layer5/issues/8257) | Reviewed "no changes needed" · awaiting merge |
| [#8280 — Heading 1 design token stays in viewport on mobile](https://github.com/layer5io/layer5/pull/8280) | 6rem default heading overflowed phones — fixes [#8267](https://github.com/layer5io/layer5/issues/8267) | Reviewed "no changes needed" · awaiting merge |
| [#8281 — carousel arrows visible and clickable on mobile](https://github.com/layer5io/layer5/pull/8281) | Arrows flickered, clipped off-screen at ≤ 850px — fixes [#8275](https://github.com/layer5io/layer5/issues/8275) | Reviewed "no changes needed" · awaiting merge |

All DCO-signed from fresh upstream branches; live previews deployed by the project's CI.

### mem0 — agent memory library

| Pull request | What it fixes | Status |
|---|---|---|
| [#7795 — close owned pgvector connection pools on `Memory.close()`](https://github.com/mem0ai/mem0/pull/7795) | Connection-pool leak; also fixed `__del__` closing caller-supplied pools — fixes [#7771](https://github.com/mem0ai/mem0/issues/7771) | Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |
| [#7797 — apply every operator on multi-operator Qdrant filters (TS SDK)](https://github.com/mem0ai/mem0/pull/7797) | `ne`/`nin` merged into one clause; `AND` branches overwrote each other — fixes [#7762](https://github.com/mem0ai/mem0/issues/7762) | Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |

mem0's flow requires the linked issue to carry an `accepted` label before PRs are reviewed — both fixes and their tests are complete and waiting on that triage.

---

## Phase 2 — New projects: reflex, agno & ollama-python

Second phase: two more projects, found by verifying merge culture live (do external contributors actually get PRs merged?), then finding bugs by code inspection.

### reflex — Python web framework compiling to React

| Pull request | What it fixes | Status |
|---|---|---|
| [#7701 — keep literal `reflex.Var` tag text from hanging or corrupting string vars](https://github.com/reflex-dev/reflex/pull/7701) | Any string prop containing literal `<reflex.Var>…</reflex.Var>` text hung the compiler in an infinite loop, crashed with `KeyError`/`IndexError`, or silently lost the text in rendered output | Open · passed two rounds of automated review · awaiting human review |
| [#7703 — `rx.asset(shared=True)` crash on Windows without Developer Mode](https://github.com/reflex-dev/reflex/pull/7703) | Symlink creation denied → whole app failed to compile; fix falls back to hardlink, then to a writable copy, keeping later compiles replaceable | Open · passed three rounds of automated review · awaiting human review |
| [#7704 — `ln()` creates the link at dest pointing to src](https://github.com/reflex-dev/reflex/pull/7704) | The public path helper did the exact opposite of `ln -s` semantics, and `overwrite=True` never worked for files | Open · passed three rounds of automated review · awaiting human review |

The #7701 review process in numbers: 5 findings from two independent AI reviewers, all confirmed real and fixed with regression tests the same day — including a quadratic-rescan trap my first fix introduced, which the reviewers caught and the final fix eliminated (measured linear: 80k pathological inputs in ~20 ms).

| Bug report | What it documents | Status |
|---|---|---|
| [#7705 — hardlink/copy fallback assets aren't cleaned up when sources vanish](https://github.com/reflex-dev/reflex/issues/7705) | Design question with three solution options; tracked in the project's internal backlog (ENG-13670) | Awaiting maintainer decision |

### agno — agent framework

| Bug report | What it documents | Status |
|---|---|---|
| [#787 — `Tool.model_dump()` leaks the `defs` field name instead of `$defs`](https://github.com/ollama/ollama-python/issues/787) | Verified serialization asymmetry between direct dumps and request-path dumps; two fix options documented for maintainers | Awaiting maintainer decision — PR offered |
| [#11414 — `LinearTools.update_issue` rejects its own documented call](https://github.com/agno-agi/agno/issues/11414) | GraphQL `$title: String!` non-null variable bound to `None` — the documented "title unchanged" call always fails; state updates advertised but impossible | Under triage — fix + 6 tests ready on a branch |
| [#11415 — `custom_scrape_website` returns field names instead of scraped data](https://github.com/agno-agi/agno/issues/11415) | Dict-key iteration returned the query's schema instead of the page content; also repaired the module's broken test fixtures and revived a maintainer-skipped test | Under triage — fix + tests ready on a branch |

agno's flow requires the issue to be labeled `ready` before PRs are reviewed — both fixes are complete and the pull requests open the moment triage lands.

---

### ollama-python — official Ollama client

| Pull request | What it fixes | Status |
|---|---|---|
| [#784 — skip blank lines in streaming NDJSON responses](https://github.com/ollama/ollama-python/pull/784) | A blank line anywhere in a streamed body (proxies, compatible servers re-chunking responses) crashed `generate(stream=True)` / `chat(stream=True)` with a raw `JSONDecodeError` | Open · awaiting review |
| [#785 — union tool parameter types serialize as a JSON Schema type array](https://github.com/ollama/ollama-python/pull/785) | Union parameter types produced an invalid comma-joined `type` (`"string, integer"`), nondeterministically ordered | Open · awaiting review |
| [#786 — `Message.get` aligned with `__contains__` semantics](https://github.com/ollama/ollama-python/pull/786) | Declared-but-unset fields returned `None` instead of the caller's default, and non-field names leaked through `.get()` | Open · awaiting review |

Found by code inspection of the streaming paths and reproduced with a blank-line-padded response; regression tests cover both the sync and async clients over a real local HTTP server.

---

## What's next

- Land the three reflex pull requests through human review — all are bot-clean with zero unresolved threads.
- Open the two agno pull requests as soon as their issues are triaged.
- Track mem0/crewAI/fastmcp/layer5/ollama-python PRs to merge and update statuses here.
- Keep the loop going: new projects entered only after verifying their merge culture live, new bugs found by reading code, every fix carrying a failing-first regression test.

---

*This page is the running index — it updates as pull requests move through review and merge, in the order the work happened.*
