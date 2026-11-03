# Open Source Contributions — Ayush (AP24110011695)

One link with everything I ship to open source. Every pull request, bug report and fix below is real, linked, and verifiable — no screenshots-only portfolio.

**About me:** B.Tech CSE student. Python / C++ / React / FastAPI. I contribute to projects in the AI-agents, MCP, developer-tools and web-framework space — picking real bugs, writing failing regression tests first, and seeing fixes through review.

**Snapshot:** 35 pull requests across 12 projects — 2 merged, 28 under review, 3 gated on mem0 triage, 1 withdrawn as a duplicate, 1 closed in favor of an assigned fix — · 12 bug reports filed · fixes passing CI and reviewed by maintainers · merges tracked here as they land.

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

## Merged

| Pull request | What it fixes | Project |
|---|---|---|
| [#677 — reject whitespace-only API key names](https://github.com/nikhilb2/simple_invoicing/pull/677) | `POST /api/api-keys/` saved a name of only spaces as an empty string; now returns 422 — merged within the hour of opening | simple_invoicing |
| [#678 — reject blank units and unknown statuses on product update](https://github.com/nikhilb2/simple_invoicing/pull/678) | Product updates silently accepted a blank unit and any status string; now reuses the create-path unit validation and bounds status to active/inactive with 422s — merged the same day, after addressing a maintainer change request with the requested API-level test | simple_invoicing |

---

## Phase 1 — First contributions across four projects

The plan: learn four different contribution cultures end to end — an AI agent framework, an MCP server framework, a cloud-native UI project, and an agent-memory library.

### crewAI — AI agent framework

| Pull request | What it fixes | Status |
|---|---|---|
| [#8845 — store sqlite checkpoint data as plain text](https://github.com/crewAIInc/crewAI/pull/8845) | Checkpoint writes crash on SQLite < 3.45 (`no such function: jsonb`) — fixes [#8843](https://github.com/crewAIInc/crewAI/issues/8843) | Open · CI green · in review |
| [#8848 — publish JSON checkpoints atomically](https://github.com/crewAIInc/crewAI/pull/8848) | Interrupted writes left truncated/corrupt checkpoint files — fixes [#8846](https://github.com/crewAIInc/crewAI/issues/8846) | Open · CI green · in review |
| [#8849 — tolerate malformed tool-call arguments in history replay](https://github.com/crewAIInc/crewAI/pull/8849) | Uncaught `JSONDecodeError` crash replaying Anthropic/Bedrock conversations — fixes [#8847](https://github.com/crewAIInc/crewAI/issues/8847) | Open · CI green · in review |

All three bugs were found by code inspection (the issues are mine too), with security review from the project's bot reporting no findings. Both atomic-write and plain-text fixes were re-validated against the project's monorepo refactor (they remain needed on the new `state/provider` paths).

### fastmcp — MCP server framework

| Pull request | What it fixes | Status |
|---|---|---|
| [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) | JSON-pointer-escaped schema names broke schema extraction — fixes [#6034](https://github.com/PrefectHQ/fastmcp/issues/6034) | Open · awaiting maintainer issue assignment |
| [#6185 — keep `tools/list` working when a root `$ref` resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | Whole-server tools listing crashed on valid schemas — fixes [#6125](https://github.com/PrefectHQ/fastmcp/issues/6125) | Open · awaiting maintainer issue assignment |
| [#6187 — support non-identifier variables in URI templates](https://github.com/PrefectHQ/fastmcp/pull/6187) | `{$top}`-style template variables never matched or forwarded; Unicode word characters that identifiers reject also disabled templates | Open · two bot-review rounds, findings fixed same day · awaiting maintainer issue assignment |
| [#6188 — keep result hydration faithful for union coercions](https://github.com/PrefectHQ/fastmcp/pull/6188) | `0 → False`-style coercions silently replaced typed results; final guard also preserves schema-intended `format: json` decodes and rejects precision-losing timestamp truncation | Open · two bot-review rounds, findings fixed same day · awaiting maintainer issue assignment |
| [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) | Tags added by a server's `tools` config were invisible to `include_tags`/`exclude_tags` on single-server MCPConfigs — fixes [#6196](https://github.com/PrefectHQ/fastmcp/issues/6196) | Open · triage bot found no defects, verified fail→pass |

1,400+ existing tests pass on each; every automated-review finding across these PRs (triage-reviewer and codex rounds) was confirmed real and fixed the same day, with the fixes re-verified against each reviewer's own fail→pass standard.

### layer5 — cloud-native UI

| Pull request | What it fixes | Status |
|---|---|---|
| [#8277 — case-study banner fits its container on mobile](https://github.com/layer5io/layer5/pull/8277) | Logo/graphic overflowed on small viewports — fixes [#8272](https://github.com/layer5io/layer5/issues/8272) | Reviewed "no changes needed" · awaiting merge |
| [#8278 — pricing cards reference real tier names](https://github.com/layer5io/layer5/pull/8278) | Bylines named tiers that don't exist ("Free", "Team") — fixes [#8258](https://github.com/layer5io/layer5/issues/8258) | Reviewed "no changes needed" · awaiting merge |
| [#8279 — Sistent icons docs: valid imports, preview matches snippet](https://github.com/layer5io/layer5/pull/8279) | Docs snippet imported non-existent exports; preview didn't match the code — fixes [#8257](https://github.com/layer5io/layer5/issues/8257) | Reviewed "no changes needed" · closed in favor of the maintainer-assigned [#8291](https://github.com/layer5io/layer5/pull/8291), which merged |
| [#8280 — Heading 1 design token stays in viewport on mobile](https://github.com/layer5io/layer5/pull/8280) | 6rem default heading overflowed phones — fixes [#8267](https://github.com/layer5io/layer5/issues/8267) | Reviewed "no changes needed" · awaiting merge |
| [#8281 — carousel arrows visible and clickable on mobile](https://github.com/layer5io/layer5/pull/8281) | Arrows flickered, clipped off-screen at ≤ 850px — fixes [#8275](https://github.com/layer5io/layer5/issues/8275) | Reviewed "no changes needed" · awaiting merge |

All DCO-signed from fresh upstream branches; live previews deployed by the project's CI.

### mem0 — agent memory library

| Pull request | What it fixes | Status |
|---|---|---|
| [#7795 — close owned pgvector connection pools on `Memory.close()`](https://github.com/mem0ai/mem0/pull/7795) | Long-running hosts ran out of Postgres connections; now self-contained: `PGVector.close()` + ownership tracking + the `Memory.close()` wiring + a live-server regression test — fixes [#7771](https://github.com/mem0ai/mem0/issues/7771). Verified in production by the issue reporter | Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |
| [#7797 — apply every operator on multi-operator Qdrant filters (TS SDK)](https://github.com/mem0ai/mem0/pull/7797) | `ne`/`nin` merged into one clause; `AND` branches overwrote each other — fixes [#7762](https://github.com/mem0ai/mem0/issues/7762) | Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |
| [#7808 — honor explicitly configured default user_id in the Hermes plugin](https://github.com/mem0ai/mem0/pull/7808) | Placeholder-collapse made an explicitly chosen default pool unreachable; gateway-native ids stranded memories — fixes [#7799](https://github.com/mem0ai/mem0/issues/7799) | Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |

mem0's flow requires the linked issue to carry an `accepted` label before PRs are reviewed — all three fixes and their tests are complete and waiting on that triage. #7795 has also been verified against the reporter's live production gateway.

---

## Phase 2 — New projects: reflex, agno & ollama-python

Second phase: two more projects, found by verifying merge culture live (do external contributors actually get PRs merged?), then finding bugs by code inspection.

### reflex — Python web framework compiling to React

| Pull request | What it fixes | Status |
|---|---|---|
| [#7701 — keep literal `reflex.Var` tag text from hanging or corrupting string vars](https://github.com/reflex-dev/reflex/pull/7701) | Any string prop containing literal `<reflex.Var>…</reflex.Var>` text hung the compiler in an infinite loop, crashed with `KeyError`/`IndexError`, or silently lost the text in rendered output | Open · passed two rounds of automated review · awaiting human review |
| [#7703 — `rx.asset(shared=True)` crash on Windows without Developer Mode](https://github.com/reflex-dev/reflex/pull/7703) | Symlink creation denied → whole app failed to compile; fix falls back to hardlink, then to a writable copy, keeping later compiles replaceable | Open · passed three rounds of automated review · awaiting human review |
| [#7704 — `ln()` creates the link at dest pointing to src](https://github.com/reflex-dev/reflex/pull/7704) | The public path helper did the exact opposite of `ln -s` semantics, and `overwrite=True` never worked for files | Open · passed three rounds of automated review · awaiting human review |
| [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) | The array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds — follow-up to #7691 | Open · awaiting review |

The #7701 review process in numbers: 5 findings from two independent AI reviewers, all confirmed real and fixed with regression tests the same day — including a quadratic-rescan trap my first fix introduced, which the reviewers caught and the final fix eliminated (measured linear: 80k pathological inputs in ~20 ms).

| Bug report | What it documents | Status |
|---|---|---|
| [#7705 — hardlink/copy fallback assets aren't cleaned up when sources vanish](https://github.com/reflex-dev/reflex/issues/7705) | Design question with three solution options; tracked in the project's internal backlog (ENG-13670) | Awaiting maintainer decision |

### agno — agent framework

| Bug report | What it documents | Status |
|---|---|---|
| [#11414 — `LinearTools.update_issue` rejects its own documented call](https://github.com/agno-agi/agno/issues/11414) | GraphQL `$title: String!` non-null variable bound to `None` — the documented "title unchanged" call always fails; state updates advertised but impossible | Reported · community contributor implementing; our fix + 6 tests staged |
| [#11415 — `custom_scrape_website` returns field names instead of scraped data](https://github.com/agno-agi/agno/issues/11415) | Dict-key iteration returned the query's schema instead of the page content; also repaired the module's broken test fixtures and revived a maintainer-skipped test | Reported · community contributor implementing; our fix + tests staged |
| [#11421 — toolkit HTTP calls without a timeout can hang the agent thread](https://github.com/agno-agi/agno/issues/11421) | `requests` call sites in 2 toolkits (ModelsLab, Linear) wait forever on a degraded upstream — scope corrected after a community fact-check confirmed Bright Data/Serply were already fixed | Reported · handed to a community contributor with the corrected scope |

agno's flow requires the issue to be labeled `ready` before PRs are reviewed — the fixes are complete and the pull requests open the moment triage lands.

---

### ollama-python — official Ollama client

| Pull request | What it fixes | Status |
|---|---|---|
| [#784 — skip blank lines in streaming NDJSON responses](https://github.com/ollama/ollama-python/pull/784) | A blank line anywhere in a streamed body (proxies, compatible servers re-chunking responses) crashed `generate(stream=True)` / `chat(stream=True)` with a raw `JSONDecodeError` | Open · awaiting review |
| [#785 — union tool parameter types serialize as a JSON Schema type array](https://github.com/ollama/ollama-python/pull/785) | Union parameter types produced an invalid comma-joined `type` (`"string, integer"`), nondeterministically ordered | Open · awaiting review |
| [#786 — `Message.get` aligned with `__contains__` semantics](https://github.com/ollama/ollama-python/pull/786) | Declared-but-unset fields returned `None` instead of the caller's default, and non-field names leaked through `.get()` | Open · awaiting review |
| [#788 — `ResponseError` survives non-object JSON error bodies](https://github.com/ollama/ollama-python/pull/788) | A gateway/proxy error body of `null`, `[]`, or a bare JSON string crashed error construction with `AttributeError`, masking the real HTTP failure | Open · awaiting review |

Found by code inspection of the streaming and error paths and reproduced over a real local HTTP server; regression tests cover both the sync and async clients.

| Bug report | What it documents | Status |
|---|---|---|
| [#787 — `Tool.model_dump()` leaks the `defs` field name instead of `$defs`](https://github.com/ollama/ollama-python/issues/787) | Verified serialization asymmetry between direct dumps and request-path dumps; two fix options documented for maintainers | Awaiting maintainer decision — PR offered |

### Powertools for AWS Lambda (Python) — AWS Lambda utility library

| Pull request | What it fixes | Status |
|---|---|---|
| [#8757 — ignore malformed `POWERTOOLS_PARAMETERS_MAX_AGE` instead of crashing](https://github.com/aws-powertools/powertools-lambda-python/pull/8757) | An empty or non-integer cache-TTL environment variable raised a raw `ValueError` from all 12 Parameters/Secrets/AppConfig entry points before any AWS call; now warns and falls back to the documented default per the project's compatibility ADR | Open · bug confirmed and assigned by a maintainer within ~2.5h of the report · milestone 3.41.0 — fixes [#8747](https://github.com/aws-powertools/powertools-lambda-python/issues/8747) |

### Actual Budget — personal finance app

| Pull request | What it fixes | Status |
|---|---|---|
| [#9416 — reject amounts too large for safe arithmetic on import](https://github.com/actualbudget/actual/pull/9416) | Importing a CSV whose amount overflows the safe-integer range crashed the transaction list on render; the import preview now rejects such rows like other unparseable fields — fixes [#9415](https://github.com/actualbudget/actual/issues/9415) | Open · all CI green · every review thread resolved · in review |
| [#9419 — return focus to the input after picking a calendar day](https://github.com/actualbudget/actual/pull/9419) | Picking a date in the calendar dropped keyboard focus, forcing mouse-only transaction entry — fixes [#9370](https://github.com/actualbudget/actual/issues/9370) | Open · in review |

### rai-toolkit (Weights & Biases) — responsible-AI evaluation toolkit

| Pull request | What it fixes | Status |
|---|---|---|
| [#130 — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130) | `rai assess <model-ref>` crashed with raw Python tracebacks for malformed refs, missing modules, and missing classes — now a clean input error matching the CLI's established convention — fixes [#129](https://github.com/wandb/rai-toolkit/issues/129) | Open · failing-first tests · awaiting review |

### ECMWF WeatherGenerator — machine-learning weather forecasting model

| Pull request | What it fixes | Status |
|---|---|---|
| [#3028 — TrainLogger takes run_id and results path instead of the global config](https://github.com/ecmwf/WeatherGenerator/pull/3028) | The training logger held the entire global config object but only ever read the run id from it — now it takes the two parameters it needs and can be used standalone — fixes the remaining scope of [#1213](https://github.com/ecmwf/WeatherGenerator/issues/1213) | Open · CI green · in review |
| [#3030 — fix legacy metrics lookup level](https://github.com/ecmwf/WeatherGenerator/pull/3030) | The metrics-file backwards-compatibility branch probed a path no released version ever wrote, so reading any pre-rename run crashed with `FileNotFoundError` instead of using the compat file — fixes [#3029](https://github.com/ecmwf/WeatherGenerator/issues/3029), a self-found bug traced through the #601/#1831 history | Open · CI green · in review |
| [#3032 — fix bare-path config entries in compare_run_configs](https://github.com/ecmwf/WeatherGenerator/pull/3032) | The config-comparison tool's bare-path format crashed with a doubled directory path ever since a config-loader fix changed `model_path` semantics — fixes [#3031](https://github.com/ecmwf/WeatherGenerator/issues/3031), self-found and reproduced end-to-end before filing | Open · in review |

Found through the good-first-issue queue after verifying the merge culture live: the project's last 10 merged pull requests came from ~8 different outside contributors. Picked up #1213's remaining requirement after auditing all three against the current code (two were already satisfied by earlier refactors — documented in the PR) and added the logger's first regression test, proven failing on the old API. The two follow-up fixes came from tracing historical PRs that changed path semantics and reproducing the broken behavior end-to-end before filing — each with fail-first regression tests, including the config-comparison tool's first tests.

### NiceGUI — Python UI framework

| Pull request | What it fixes | Status |
|---|---|---|
| [#6468 — fix missing Torus export from the scene objects package](https://github.com/zauberzeug/nicegui/pull/6468) | `Torus` shipped in 3.19.0 with a scene method but the objects package forgot the import and `__all__` entry, so the documented import path raised `ImportError` — plus a package-wide export-consistency test so the next new object can't be forgotten | Open · in review |

Selected through a data-backed vetting pipeline (merge culture measured over the last 60 days, release cadence, AI policies read in full, labeled-issue queues verified claimable) alongside two more projects now in the rotation: Arize-ai/phoenix (AI observability) and pypdf — the latter with an explicit AI-assistance policy in its contributing guide.

---

## What's next

- Land the four reflex pull requests through human review — all are bot-clean with zero unresolved threads.
- Open the two agno pull requests as soon as their issues are triaged.
- Track mem0/crewAI/fastmcp/layer5/ollama-python PRs to merge and update statuses here.
- Keep the loop going: new projects entered only after verifying their merge culture live, new bugs found by reading code, every fix carrying a failing-first regression test.

---

*This page is the running index — it updates as pull requests move through review and merge, in the order the work happened.*
