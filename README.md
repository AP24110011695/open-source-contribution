# Open Source Contributions — Ayush (AP24110011695)

I find and fix real bugs in production open-source projects — by reading the code, writing the failing test first, and shipping small, reviewed changes. Everything on this page is real and linked.

**10 PRs merged** · **30 projects** · **6 reviews of other contributors' PRs (3 approvals)** — across PyPA, Apache, CNCF, the Linux Foundation, Meta, AWS, ECMWF and Weights & Biases

Languages & domains: Python · Go · Java · Rust · C/C++ · TypeScript — CLI tooling, PDF parsing, ML infrastructure, data formats, CI & packaging, monitoring, pub-sub messaging

🟢 in review · 🟡 waiting on a maintainer · 🔒 gated on triage · ⚪ closed

---

## Highlights

**[pipx (PyPA) — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423)**
`pipx repair` reported environments whose metadata a killed install had lost as "healthy" (exit 0), while the project's own reinstall flow refuses them — so a user following `pipx list`'s fix advice got a silent no-op. Self-found by auditing the killed-install hardening series for the command its changelog promised but never wired. **Approved by the maintainer within the hour, merged the same night.**

**[pipx (PyPA) — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431)**
Every repeat `pipx ensurepath` run claimed it had appended directories to PATH when they were already there — reporting a change that never happened and pointing users at `--force` for nothing. **Merged by the lead maintainer with the `bug` label, 27 checks green.**

**[pypdf — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353)**
Two code paths still crashed with `TypeError` on malformed PDFs — the same robustness class the project had already fixed twice elsewhere; located by mining that repeated fix pattern for unfixed siblings. **Merged after the full review cycle** — coverage requested and covered, five maintainer suggestions applied, two of them test-proven corrections to the suggestions themselves.

**[fastmcp — keep tools/list working when a root $ref resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185)**
A valid JSON Schema (`$ref` resolving to `true`/`false`) crashed whole-server tool listing during client init. **Merged with two sibling fixes in the same batch** — URI-template variables and tag-filter ordering — four merges in one day.

**[fastmcp — decode RFC 6901 escapes when extracting $defs names](https://github.com/PrefectHQ/fastmcp/pull/6180)**
JSON-pointer-escaped schema names (`foo/bar`, `a~b`) broke schema extraction; the maintainer finalized the branch himself before merging.

**[rai-toolkit (Weights & Biases) — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130)**
`rai assess <model-ref>` answered malformed refs, missing modules and missing classes with raw Python tracebacks; now a clean input error, while a valid model's own failures keep their original traceback. **Merged after a full human review cycle** — changes requested on the exception boundary, corrected to the maintainer's spec, approved.

**[reflex — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707)**
The array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds. **Approved and merged by the maintainer.**

---

## How I work

- I find most bugs myself by reading the code — the issues behind them are mine too, not ones I picked off a shelf. Example: the pypdf guards came from noticing the project had fixed the same crash class twice and asking which call sites were still missing.
- Every fix starts with a small failing test on the project's own `main`, to prove the bug is real. Then the fix, and the same test passing. Example: the pipx `ensurepath` claim was reproduced by running the command twice and comparing what it printed against what actually changed.
- I read each project's contribution rules before opening anything — sign-offs, issue gates, PR templates — so nothing I send breaks their flow.
- Every pull request explains the root cause and links the issue it fixes.
- When a reviewer leaves feedback, I fix it the same day and reply with the commit that addresses it.
- When I approve someone else's pull request, it's because I checked out their branch, ran the tests, and reproduced the bug on the unfixed code first — not because the diff looked fine.
- Tests mock real external services — never the code under test.

---

## Merged

| Pull request | What it fixes | Project |
|---|---|---|
| [#677 — reject whitespace-only API key names](https://github.com/nikhilb2/simple_invoicing/pull/677) | `POST /api/api-keys/` saved a name of only spaces as an empty string; now returns 422 — merged within the hour of opening | simple_invoicing |
| [#678 — reject blank units and unknown statuses on product update](https://github.com/nikhilb2/simple_invoicing/pull/678) | Product updates silently accepted a blank unit and any status string; now reuses the create-path unit validation and bounds status to active/inactive with 422s — merged the same day, after addressing a maintainer change request with the requested API-level test | simple_invoicing |
| [#130 — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130) | `rai assess <model-ref>` crashed with raw Python tracebacks for malformed refs, missing modules, and missing classes — now a clean input error, while a valid model's own factory or constructor failures keep their original exception and traceback — merged after a full human review cycle: changes requested on the exception boundary, corrected to the maintainer's spec, approved | rai-toolkit (Weights & Biases) |
| [#2423 — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423) | `pipx repair` reported environments whose `pipx_metadata.json` a killed install lost as "healthy" (exit 0), even though the project's own #2234 hardening makes `pipx reinstall` and `pipx reinstall-all` refuse them — the repair flow could only reach that refusal through a broken interpreter, so a still-running one silenced it and a user following `pipx list`'s fix advice got a silent no-op — approved by the maintainer within the hour, merged the same night | pipx (PyPA) |
| [#2431 — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431) | every repeat `pipx ensurepath` run claimed "all pipx binary directories have been appended to PATH" when nothing was appended — the directories were already in PATH, so the summary reported a change that did not happen and pointed users at `--force`; reworded to report the true state and the `--force`/`--prepend` way to re-add, with the summary checking every directory before making the claim — merged by the lead maintainer with the `bug` label | pipx (PyPA) |
| [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) | the array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds; approved and merged by the maintainer | reflex |
| [#4353 — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353) | two code paths still crashed with `TypeError` when a page's `/Resources` was not a dictionary — the font walk and the inline-image color-space lookup, siblings of fixes #4272/#4329; warn-and-treat-as-empty guards with regression tests covering the crash, the resolution, and the null branches — merged after the full review cycle: coverage requested and covered, five suggestions applied (two of them test-proven corrections to the suggestions themselves) | pypdf |
| [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) | single-server `MCPConfig` applied include/exclude tags before the tools transform, so transform-added tags were invisible to the filter — reordered to match the composite-server path; verified with a platform-independent in-process regression test | fastmcp |
| [#6187 — make resource templates for non-identifier path parameters readable](https://github.com/PrefectHQ/fastmcp/pull/6187) | non-identifier path parameters produced unreadable sanitized resource-template names; templated expansion now emits valid identifiers while preserving the original path parameters | fastmcp |
| [#6185 — keep tools/list working when a root $ref resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | a JSON Schema root `$ref` resolving to `true`/`false` crashed `tools/list` during client init; the dereference path now handles boolean root schemas | fastmcp |

---

## Code reviews — other contributors' pull requests

I also review pull requests from other contributors in Apache projects. An approval from me means I checked out the branch, ran the tests, and reproduced the bug being fixed on the unfixed code first.

| Review | What I verified | Outcome |
|---|---|---|
| [#4292 — apply every delete file when rewriting files for a partial delete](https://github.com/apache/iceberg-python/pull/4292#pullrequestreview-5807190431) — PyIceberg | a partial delete could resurrect deleted rows when filtered reads bounds-prune delete files — confirmed the fix's rationale, ran the new test across three catalog fixtures, reproduced the exact deleted-rows-returning failure on the unfixed code, and ran the 721-test behavior regression slice | ✅ Approved — failure reproduced fail-first locally |
| [#4529 — fail MonitorServiceTest if nothing throws](https://github.com/apache/hertzbeat/pull/4529#pullrequestreview-5805159800) — HertzBeat | read all 11 try/catch → assertThrows conversions, ran the test module locally (71/71 green), then did an independent mutation check: commenting out a real throw in the service made the new test fail — proving the old pattern would have passed silently | ✅ Approved — 71/71 green locally + mutation check |
| [#4296 — read a file without avro.codec as uncompressed](https://github.com/apache/iceberg-python/pull/4296#pullrequestreview-5804767229) — PyIceberg | ran the new codec tests on the branch and reproduced the pre-fix failure (`Unsupported codec: gzip`) on the old code, then mapped every config-fallback site the one-line change touches | ✅ Approved — fail-first reproduced locally |
| [#4289 — skip unknown nested fields when resolving Avro read schemas](https://github.com/apache/iceberg-python/pull/4289#pullrequestreview-5790634073) — PyIceberg | ran the PR's own test locally and probed all four type-mismatch guarantees (map-vs-string, list-vs-map, top-level and field-level) still raise | 💬 Commented — suggested a field-level mismatch regression test |
| [#4526 — add the missing SSL parameter to HDFS NameNode/DataNode/YARN](https://github.com/apache/hertzbeat/pull/4526#pullrequestreview-5790679437) — HertzBeat | traced the diagnosis end-to-end (the placeholder survives substitution, so `Boolean.parseBoolean` always answers false), then scope-checked it: grepped all 40 templates using the SSL placeholder — the PR's 3 files are the complete set | 💬 Commented — confirmed the scope is complete |
| [#76629 — DAG-level on_failure_callback dropped on detached session errors](https://github.com/apache/airflow/pull/76629#pullrequestreview-5807222864) — Airflow | verified the exception-catch hierarchy statically (`PendingRollbackError`/`InvalidRequestError` both escape the `DetachedInstanceError`-only catch) and flagged a sibling path pruning entries the same way | 💬 Commented — same-class sibling flagged |

---

## The full log — by project

**PyPA** — [pipx](#pipx) · [wheel](#wheel) · [cibuildwheel](#cibuildwheel)

**Apache** — [PyIceberg](#iceberg) · [Airflow](#airflow) · [HertzBeat](#hertzbeat) · [OpenDAL](#opendal) · [Pulsar](#pulsar) · [Superset](#superset)

**CNCF** — [Dapr](#dapr) · [Argo CD](#argocd)

**Linux Foundation** — [Zephyr RTOS](#zephyr) · [osquery](#osquery) · [ONNX](#onnx) · [ONNX precision](#onnx-fp32)

**Meta** — [PyTorch](#pytorch-core) · [BoTorch](#botorch)

**More** — [crewAI](#crewai) · [fastmcp](#fastmcp) · [layer5](#layer5) · [mem0](#mem0) · [reflex](#reflex) · [agno](#agno) · [ollama-python](#ollama) · [Powertools for AWS](#powertools) · [Actual Budget](#actual) · [ECMWF WeatherGenerator](#weathergen) · [pypdf](#pypdf) · [NiceGUI](#nicegui)

---

<a name="crewai"></a>

## <img src="https://github.com/crewAIInc.png" width="24" alt="crewAI"> crewAI

| Pull request | What it fixes | Status |
|---|---|---|
| [#8845 — store sqlite checkpoint data as plain text](https://github.com/crewAIInc/crewAI/pull/8845) | Checkpoint writes crash on SQLite < 3.45 (`no such function: jsonb`) — fixes [#8843](https://github.com/crewAIInc/crewAI/issues/8843) | 🟢 Open · CI green · in review |
| [#8848 — publish JSON checkpoints atomically](https://github.com/crewAIInc/crewAI/pull/8848) | Interrupted writes left truncated/corrupt checkpoint files — fixes [#8846](https://github.com/crewAIInc/crewAI/issues/8846) | 🟢 Open · CI green · in review |
| [#8849 — tolerate malformed tool-call arguments in history replay](https://github.com/crewAIInc/crewAI/pull/8849) | Uncaught `JSONDecodeError` crash replaying Anthropic/Bedrock conversations — fixes [#8847](https://github.com/crewAIInc/crewAI/issues/8847) | 🟢 Open · CI green · in review |

<a name="fastmcp"></a>

## <img src="https://github.com/PrefectHQ.png" width="24" alt="fastmcp"> fastmcp

| Pull request | What it fixes | Status |
|---|---|---|
| [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) | JSON-pointer-escaped schema names broke schema extraction — fixes [#6034](https://github.com/PrefectHQ/fastmcp/issues/6034) | ✅ Merged — maintainer finalized the branch himself before merging |
| [#6440 — compare pinned tool versions PEP 440-normalized against the listed version](https://github.com/PrefectHQ/fastmcp/pull/6440) | calling a versioned tool by an equivalent version spelling (`"1"` for a listed `"1.0"`, `"v1.0"`) ran the listed tool but silently skipped output-schema hydration and result revalidation, because the client compared versions as strings while the server matches PEP 440-normalized — fixes [#6439](https://github.com/PrefectHQ/fastmcp/issues/6439) | 🔒 Gated by the require-issue-link bot until the issue is assigned |
| [#6185 — keep `tools/list` working when a root `$ref` resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | Whole-server tools listing crashed on valid schemas — fixes [#6125](https://github.com/PrefectHQ/fastmcp/issues/6125) | ✅ Merged |
| [#6187 — support non-identifier variables in URI templates](https://github.com/PrefectHQ/fastmcp/pull/6187) | `{$top}`-style template variables never matched or forwarded; Unicode word characters that identifiers reject also disabled templates | ✅ Merged |
| [#6188 — keep result hydration faithful for union coercions](https://github.com/PrefectHQ/fastmcp/pull/6188) | `0 → False`-style coercions silently replaced typed results; final guard also preserves schema-intended `format: json` decodes and rejects precision-losing timestamp truncation | 🟡 Open · survived three adversarial review rounds with same-session fixes · awaiting human review |
| [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) | Tags added by a server's `tools` config were invisible to `include_tags`/`exclude_tags` on single-server MCPConfigs — fixes [#6196](https://github.com/PrefectHQ/fastmcp/issues/6196) | ✅ Merged |

<a name="layer5"></a>

## <img src="https://github.com/layer5io.png" width="24" alt="layer5"> layer5

| Pull request | What it fixes | Status |
|---|---|---|
| [#8277 — case-study banner fits its container on mobile](https://github.com/layer5io/layer5/pull/8277) | Logo/graphic overflowed on small viewports — fixes [#8272](https://github.com/layer5io/layer5/issues/8272) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8278 — pricing cards reference real tier names](https://github.com/layer5io/layer5/pull/8278) | Bylines named tiers that don't exist ("Free", "Team") — fixes [#8258](https://github.com/layer5io/layer5/issues/8258) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8279 — Sistent icons docs: valid imports, preview matches snippet](https://github.com/layer5io/layer5/pull/8279) | Docs snippet imported non-existent exports; preview didn't match the code — fixes [#8257](https://github.com/layer5io/layer5/issues/8257) | ⚪ Reviewed "no changes needed" · closed in favor of the maintainer-assigned [#8291](https://github.com/layer5io/layer5/pull/8291), which merged |
| [#8280 — Heading 1 design token stays in viewport on mobile](https://github.com/layer5io/layer5/pull/8280) | 6rem default heading overflowed phones — fixes [#8267](https://github.com/layer5io/layer5/issues/8267) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8281 — carousel arrows visible and clickable on mobile](https://github.com/layer5io/layer5/pull/8281) | Arrows flickered, clipped off-screen at ≤ 850px — fixes [#8275](https://github.com/layer5io/layer5/issues/8275) | 🟢 Reviewed "no changes needed" · awaiting merge |

<a name="mem0"></a>

## <img src="https://github.com/mem0ai.png" width="24" alt="mem0"> mem0

| Pull request | What it fixes | Status |
|---|---|---|
| [#7795 — close owned pgvector connection pools on `Memory.close()`](https://github.com/mem0ai/mem0/pull/7795) | Long-running hosts ran out of Postgres connections; now self-contained: `PGVector.close()` + ownership tracking + the `Memory.close()` wiring + a live-server regression test — fixes [#7771](https://github.com/mem0ai/mem0/issues/7771). Verified in production by the issue reporter | 🔒 Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |
| [#7797 — apply every operator on multi-operator Qdrant filters (TS SDK)](https://github.com/mem0ai/mem0/pull/7797) | `ne`/`nin` merged into one clause; `AND` branches overwrote each other — fixes [#7762](https://github.com/mem0ai/mem0/issues/7762) | 🔒 Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |
| [#7808 — honor explicitly configured default user_id in the Hermes plugin](https://github.com/mem0ai/mem0/pull/7808) | Placeholder-collapse made an explicitly chosen default pool unreachable; gateway-native ids stranded memories — fixes [#7799](https://github.com/mem0ai/mem0/issues/7799) | 🔒 Gated pending maintainer triage (auto-reopens when the issue is labeled `accepted`) |

<a name="reflex"></a>

## <img src="https://github.com/reflex-dev.png" width="24" alt="reflex"> reflex

| Pull request | What it fixes | Status |
|---|---|---|
| [#7701 — keep literal `reflex.Var` tag text from hanging or corrupting string vars](https://github.com/reflex-dev/reflex/pull/7701) | Any string prop containing literal `<reflex.Var>…</reflex.Var>` text hung the compiler in an infinite loop, crashed with `KeyError`/`IndexError`, or silently lost the text in rendered output | 🟡 Open · passed two rounds of automated review · awaiting human review |
| [#7703 — `rx.asset(shared=True)` crash on Windows without Developer Mode](https://github.com/reflex-dev/reflex/pull/7703) | Symlink creation denied → whole app failed to compile; fix falls back to hardlink, then to a writable copy, keeping later compiles replaceable | 🟡 Open · passed three rounds of automated review · awaiting human review |
| [#7704 — remove unused `path_ops.ln`](https://github.com/reflex-dev/reflex/pull/7704) | The public path helper did the exact opposite of `ln -s` semantics; the maintainer, on review, preferred removing it once the zero-callers search was confirmed — the PR was converted to the removal with a breaking-change changelog note | 🟡 Open · converted to removal on the maintainer's review · awaiting merge |
| [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) | The array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds — follow-up to #7691 | ✅ Merged by the maintainer |

| Bug report | What it documents | Status |
|---|---|---|
| [#7705 — hardlink/copy fallback assets aren't cleaned up when sources vanish](https://github.com/reflex-dev/reflex/issues/7705) | Design question with three solution options; tracked in the project's internal backlog (ENG-13670) | 🟡 Awaiting maintainer decision |

<a name="agno"></a>

## <img src="https://github.com/agno-agi.png" width="24" alt="agno"> agno

| Bug report | What it documents | Status |
|---|---|---|
| [#11414 — `LinearTools.update_issue` rejects its own documented call](https://github.com/agno-agi/agno/issues/11414) | GraphQL `$title: String!` non-null variable bound to `None` — the documented "title unchanged" call always fails; state updates advertised but impossible | 🟡 Reported · community contributor implementing; our fix + 6 tests staged |
| [#11415 — `custom_scrape_website` returns field names instead of scraped data](https://github.com/agno-agi/agno/issues/11415) | Dict-key iteration returned the query's schema instead of the page content; also repaired the module's broken test fixtures and revived a maintainer-skipped test | 🟡 Reported · community contributor implementing; our fix + tests staged |
| [#11421 — toolkit HTTP calls without a timeout can hang the agent thread](https://github.com/agno-agi/agno/issues/11421) | `requests` call sites in 2 toolkits (ModelsLab, Linear) wait forever on a degraded upstream — scope corrected after a community fact-check confirmed Bright Data/Serply were already fixed | 🟡 Reported · handed to a community contributor with the corrected scope |

<a name="ollama"></a>

## <img src="https://github.com/ollama.png" width="24" alt="ollama-python"> ollama-python

| Pull request | What it fixes | Status |
|---|---|---|
| [#784 — skip blank lines in streaming NDJSON responses](https://github.com/ollama/ollama-python/pull/784) | A blank line anywhere in a streamed body (proxies, compatible servers re-chunking responses) crashed `generate(stream=True)` / `chat(stream=True)` with a raw `JSONDecodeError` | 🟡 Open · awaiting review |
| [#785 — union tool parameter types serialize as a JSON Schema type array](https://github.com/ollama/ollama-python/pull/785) | Union parameter types produced an invalid comma-joined `type` (`"string, integer"`), nondeterministically ordered | 🟡 Open · awaiting review |
| [#786 — `Message.get` aligned with `__contains__` semantics](https://github.com/ollama/ollama-python/pull/786) | Declared-but-unset fields returned `None` instead of the caller's default, and non-field names leaked through `.get()` | 🟡 Open · awaiting review |
| [#788 — `ResponseError` survives non-object JSON error bodies](https://github.com/ollama/ollama-python/pull/788) | A gateway/proxy error body of `null`, `[]`, or a bare JSON string crashed error construction with `AttributeError`, masking the real HTTP failure | 🟡 Open · awaiting review |

| Bug report | What it documents | Status |
|---|---|---|
| [#787 — `Tool.model_dump()` leaks the `defs` field name instead of `$defs`](https://github.com/ollama/ollama-python/issues/787) | Verified serialization asymmetry between direct dumps and request-path dumps; two fix options documented for maintainers | 🟡 Awaiting maintainer decision — PR offered |

<a name="powertools"></a>

## <img src="https://github.com/aws-powertools.png" width="24" alt="Powertools"> Powertools for AWS Lambda (Python)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8757 — ignore malformed `POWERTOOLS_PARAMETERS_MAX_AGE` instead of crashing](https://github.com/aws-powertools/powertools-lambda-python/pull/8757) | An empty or non-integer cache-TTL environment variable raised a raw `ValueError` from all 12 Parameters/Secrets/AppConfig entry points before any AWS call; now warns and falls back to the documented default per the project's compatibility ADR | 🟢 Open · bug confirmed and assigned by a maintainer within ~2.5h of the report · milestone 3.41.0 — fixes [#8747](https://github.com/aws-powertools/powertools-lambda-python/issues/8747) |

<a name="actual"></a>

## <img src="https://github.com/actualbudget.png" width="24" alt="Actual Budget"> Actual Budget

| Pull request | What it fixes | Status |
|---|---|---|
| [#9416 — reject amounts too large for safe arithmetic on import](https://github.com/actualbudget/actual/pull/9416) | Importing a CSV whose amount overflows the safe-integer range crashed the transaction list on render; the import preview now rejects such rows like other unparseable fields — fixes [#9415](https://github.com/actualbudget/actual/issues/9415) | 🟢 Open · all CI green · every review thread resolved · in review |
| [#9419 — return focus to the input after picking a calendar day](https://github.com/actualbudget/actual/pull/9419) | Picking a date in the calendar dropped keyboard focus, forcing mouse-only transaction entry — fixes [#9370](https://github.com/actualbudget/actual/issues/9370) | 🟢 Open · in review |

<a name="weathergen"></a>

## <img src="https://github.com/ecmwf.png" width="24" alt="ECMWF"> ECMWF WeatherGenerator

| Pull request | What it fixes | Status |
|---|---|---|
| [#3028 — TrainLogger takes run_id and results path instead of the global config](https://github.com/ecmwf/WeatherGenerator/pull/3028) | The training logger held the entire global config object but only ever read the run id from it — now it takes the two parameters it needs and can be used standalone — fixes the remaining scope of [#1213](https://github.com/ecmwf/WeatherGenerator/issues/1213) | 🟢 Open · CI green · in review |
| [#3030 — fix legacy metrics lookup level](https://github.com/ecmwf/WeatherGenerator/pull/3030) | The metrics-file backwards-compatibility branch probed a path no released version ever wrote, so reading any pre-rename run crashed with `FileNotFoundError` instead of using the compat file — fixes [#3029](https://github.com/ecmwf/WeatherGenerator/issues/3029), a self-found bug traced through the #601/#1831 history | 🟢 Open · CI green · in review |
| [#3032 — fix bare-path config entries in compare_run_configs](https://github.com/ecmwf/WeatherGenerator/pull/3032) | The config-comparison tool's bare-path format crashed with a doubled directory path ever since a config-loader fix changed `model_path` semantics — fixes [#3031](https://github.com/ecmwf/WeatherGenerator/issues/3031), self-found and reproduced end-to-end before filing | 🟢 Open · in review |

<a name="pypdf"></a>

## <img src="https://github.com/py-pdf.png" width="24" alt="pypdf"> pypdf

| Pull request | What it fixes | Status |
|---|---|---|
| [#4353 — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353) | Two code paths (font listing and inline-image color-space lookup) still crashed with `TypeError` when `/Resources` was not a dictionary — the same robustness class fixed twice elsewhere in the codebase — fixes [#4352](https://github.com/py-pdf/pypdf/issues/4352), a self-found bug located by mining that repeated fix pattern | ✅ Merged — after the full review cycle: coverage requested and covered, five maintainer suggestions applied (two test-proven corrections to the suggestions themselves) |

<a name="nicegui"></a>

## <img src="https://github.com/zauberzeug.png" width="24" alt="NiceGUI"> NiceGUI

| Pull request | What it fixes | Status |
|---|---|---|
| [#6468 — fix missing Torus export from the scene objects package](https://github.com/zauberzeug/nicegui/pull/6468) | `Torus` shipped in 3.19.0 with a scene method but the objects package forgot the import and `__all__` entry, so the documented import path raised `ImportError` | ⚪ Closed — same fix already open as [#6461](https://github.com/zauberzeug/nicegui/pull/6461) by the issue reporter and scheduled for 4.1 |

<a name="iceberg"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Iceberg (PyIceberg)

| Pull request | What it fixes | Status |
|---|---|---|
| [#4285 — handle negative-scale Decimals in increment, decrement and truncate_decimal](https://github.com/apache/iceberg-python/pull/4285) | Three remaining call sites of a `Decimal` scale misread (`abs()` applied to the exponent) turned `1E+2` into `0.02` on increment — four orders of magnitude off; the same root cause was fixed elsewhere by #3997 — fixes [#4284](https://github.com/apache/iceberg-python/issues/4284), self-found by mining recently merged validation fixes for unfixed siblings | 🟢 Open · all 20 CI checks green · mergeable · in review |
| [#4287 — reject non-finite floats on conversion to Decimal](https://github.com/apache/iceberg-python/pull/4287) | An infinity float/double literal crashed `to(DecimalType)` with a bare `decimal.InvalidOperation` instead of the module's standard conversion error — fixes [#4286](https://github.com/apache/iceberg-python/issues/4286), self-found while auditing the conversion surfaces for unfixed siblings | 🟢 Open · in review |

<a name="airflow"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Airflow (Task SDK)

| Pull request | What it fixes | Status |
|---|---|---|
| [#76481 — Fix `SecretCache` export in `airflow.sdk`](https://github.com/apache/airflow/pull/76481) | `SecretCache` resolved at runtime through the lazy-import map but was missing from `__all__` and the TYPE_CHECKING re-exports, so type checkers flagged every import — including seven inside Airflow core itself; same drift class as the project's own `lineage` fix | 🟢 Open · in review |
| [#76486 — Add `__dir__` to `airflow.sdk` so `dir()` exposes the lazy public API](https://github.com/apache/airflow/pull/76486) | The module resolved its 105-name public API through `__getattr__` alone, so `dir()` — what IDEs, REPLs and tooling discover — hid the entire surface until each name was touched; PEP 562 recommends pairing `__getattr__` with a `__dir__` | 🟢 Open · in review — stacked on [#76481](https://github.com/apache/airflow/pull/76481) |

<a name="hertzbeat"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache HertzBeat (real-time monitoring)

| Pull request | What it fixes | Status |
|---|---|---|
| [#4528 — recognize default-key ciphertext in `isCiphertext` under a custom key](https://github.com/apache/hertzbeat/pull/4528) | `isCiphertext` answered `false` for data encoded with the default secret key while a custom key was configured, while `aesDecode` decrypted the same payload via its default-key fallback — so callers deciding decrypt-vs-use-as-is treated real ciphertext as plaintext (three live call sites; a fourth already worked around it) — fixes [#4527](https://github.com/apache/hertzbeat/issues/4527), self-found by mining the project's fresh credential-hardening fixes for siblings | 🟢 Open · in review |
| [#4548 — stop jdbc connection property injection through database diagnostics](https://github.com/apache/hertzbeat/pull/4548) | the 2.0 gateway diagnostics service concatenated monitor-supplied host/port/database straight into a `jdbc:mysql://` url, so `db?allowLoadLocalInfile=true` injected arbitrary driver properties — exactly the attack class `JdbcUrlSafetyUtil` was built for in #4299, whose guard set the sibling `DatabaseToolsImpl` carries but this newer call site dropped — located by auditing every call site of the guard, regression tests verified failing-first (the injected property shows up verbatim in the driver's exception pre-fix) | 🟢 Open · in review |

<a name="opendal"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache OpenDAL (data access layer)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8484 — trim whitespace in `normalize_root`](https://github.com/apache/opendal/pull/8484) | `normalize_root`'s own documented rules say whitespace is trimmed (identical wording to `normalize_path`, which trims and is pinned-tested), but the code never did — a root configured as `" my-dir "` became `"/ my-dir /"` and every object path under the backend silently carried the spaces | 🟢 Open · in review |

<a name="pulsar"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Pulsar (pub-sub messaging)

| Pull request | What it fixes | Status |
|---|---|---|
| [#27375 — handle empty values in FieldParser converters and setEmptyValue](https://github.com/apache/pulsar/pull/27375) | `stringToLong("")`/`stringToFloat("")` crashed with `NumberFormatException` while the Integer/Double siblings return `null` (their guard was never added to these two), and `setEmptyValue`'s String check compared the type object's class to `String.class` — always false — so blank values left stale Strings instead of clearing them — fixes [#27374](https://github.com/apache/pulsar/issues/27374), self-found by reading the config-parsing utilities against their own sibling patterns | 🟢 Open · in review |

| Bug report | What it documents | Status |
|---|---|---|
| [#27377 — `RelativeTimeUtil` silently fabricates values for overflow-sized inputs](https://github.com/apache/pulsar/issues/27377) | every other malformed input raises, but `"15252526452552645w"` returns a wrapped garbage value — the JDK `TimeUnit` conversion saturates at `Long.MAX_VALUE` seconds and the week/year step then wraps it; measured on the project's own compiled classes, with the fix proven fail-first through the project's gradle setup | 🟡 Filed — fix branch staged, PR opens once #27375 gets its first maintainer signal |

<a name="superset"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Superset (data visualization)

| Pull request | What it fixes | Status |
|---|---|---|
| [#46040 — reject deeply nested date expressions with a parse error](https://github.com/apache/superset/pull/46040) | `datetime_eval` converts only `ParseException`, but the date-expression grammar recurses once per nesting level — a pasted ~500-character time range (60–80 nested `dateadd(` calls, measured on master) exhausted the interpreter stack and hit the chart-data and Jinja paths as an unhandled `RecursionError` (500) instead of the parse error every other malformed expression produces — fixes [#46039](https://github.com/apache/superset/issues/46039), self-found by fix-commit mining the freshly-fixed date-parser area | 🟢 Open · in review |

<a name="dapr"></a>

## <img src="https://github.com/dapr.png" width="24" alt="Dapr"> Dapr (CNCF)

| Bug report | What it documents | Status |
|---|---|---|
| [kit #179 — ISO 8601 duration parser accepts overflowing and negative components](https://github.com/dapr/kit/issues/179) | the parser accepts hours far beyond any sane range and negative durations — downstream the scheduler builds `@every` intervals from them, a `uint32` truncation fires, and negative repeat counts never decrement; filed with a probe table after checking the project's four open parser issues for overlap | 🟡 Filed — fix PR staged behind the in-flight parser PRs |
| [#11056 — actor reminder/timer APIs panic on a `null` body](https://github.com/dapr/dapr/issues/11056#issuecomment-6691551369) | confirmed the reporter's crash with a unit probe at both panic sites and pinned the mechanism: a `*struct` unmarshal target becomes nil on JSON `null`, then a field dereference panics | 🟢 Confirmed — repro + mechanism posted |
| [#11050 — an unknown CEL expression identifier hangs daprd in an infinite compile loop](https://github.com/dapr/dapr/issues/11050#issuecomment-6691611633) | confirmed with a probe that never returns: a compile error shares its message prefix with the "missing variable" path, so the expression recompiles forever — affects pubsub routing rules and circuit-breaker expressions | 🟢 Confirmed — repro + mechanism posted |
| [#11032 — outbox PublishInternal panics on multi-projection transactions](https://github.com/dapr/dapr/issues/11032#issuecomment-6745667701) | confirmed with an in-package probe running the issue's exact 4-operation batch: the strip loop mutates `operations` while ranging over it — each in-place shift reassigns the slice to a narrower view, so a later iteration dies with `slice bounds out of range [4:2]` and entries are skipped along the way | 🟢 Confirmed — repro + mechanism posted |

<a name="zephyr"></a>

## <img src="https://github.com/zephyrproject-rtos.png" width="24" alt="Zephyr"> Zephyr RTOS (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#124926 — unlock interrupts on error paths in rx_enable](https://github.com/zephyrproject-rtos/zephyr/pull/124926) | `ifx_cat1_uart_async_rx_enable()` locked interrupts before validating its arguments and DMA state, but four error paths returned without unlocking — a caller passing a bad buffer or racing an active RX got the system frozen with interrupts disabled. Found by scanning every `irq_lock()` error path in `drivers/` after the same bug was fixed in two DMA drivers a day apart; maintainer requested a v4.5 backport — tracking issue [#124960](https://github.com/zephyrproject-rtos/zephyr/issues/124960) | 🟢 Open · maintainer engagement (backport requested) |
| [#124927 — unlock interrupts on invalid pin configurations](https://github.com/zephyrproject-rtos/zephyr/pull/124927) | Two GPIO drivers returned `-ENOTSUP` from their configure callbacks with interrupts still locked — one rejected a pin set as both input and output, the other fell through the direction switch's default arm. Both now unlock before returning | 🟢 Open · in review |
| [#124961 — unlock interrupts on USB error paths](https://github.com/zephyrproject-rtos/zephyr/pull/124961) | The Renesas RA UDC returned `-EIO` from endpoint-dequeue with interrupts still locked when transfer abort failed, and the SAM USBC attach returned the pinctrl error the same way — leaving the system frozen after a rejected attach. Both now unlock before returning | 🟢 Open · in review |
| [#124962 — unlock interrupts on grant double-free](https://github.com/zephyrproject-rtos/zephyr/pull/124962) | Xen's grant-table release path logged a warning and returned from the double-free case with interrupts still locked — a repeated release froze the system permanently. Now unlocks before returning | 🟢 Open · in review |

<a name="osquery"></a>

## <img src="https://github.com/osquery.png" width="24" alt="osquery"> osquery (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#9280 — reject truncated shellbag file-entry records instead of throwing](https://github.com/osquery/osquery/pull/9280) | `fileEntry()` subtracted 8 from the position of the `0400EFBE` signature it found anywhere in attacker-controlled shellbag data — a record starting with that signature underflowed the unsigned offset past its zero-check, and truncated records made `substr()` throw `std::out_of_range`, which the table layer turns into a failed query: one malformed registry value silently killed the entire `shellbags` query. Three guards now return the existing unsupported sentinel; found as the missed sibling of #9218's drive-item guards | 🟢 **Approved** · all CI green · awaiting merge |
| [#9283 — check netlink payload lengths before typed reads in routes](https://github.com/osquery/osquery/pull/9283) | The Linux routes table walked netlink attributes with `RTA_OK()`, which validates only the attribute *header* against the remaining bytes, then dereferenced the payloads unchecked — interface indexes, metrics and addresses were read as `int`/`inet_ntop` from buffers that could end mid-field, so a truncated final attribute read past the end of the message. Every typed read now checks `RTA_PAYLOAD()`; ships with a byte-by-byte netlink test harness (the routes table's first) whose truncated-attribute cases read past the message on master | 🟢 **Approved** · awaiting merge |
| [#9286 — reject truncated records in the remaining shellitem parsers](https://github.com/osquery/osquery/pull/9286) | Eleven more shellbag parsers read fixed-offset fields with `substr()` and could throw on attacker-controlled truncated records, aborting the whole query — the file-entry fix (#9280) left these siblings behind. Every parser now rejects under-length records with its existing sentinel; nine tests craft records that end inside each parser's field reads | 🟢 Open · in review |

<a name="onnx-fp32"></a>

## <img src="https://github.com/onnx.png" width="24" alt="ONNX"> ONNX — reference precision

| Pull request | What it fixes | Status |
|---|---|---|
| [#8772 — compute BatchNormalization training and LpNormalization in float32](https://github.com/onnx/onnx/pull/8772) | Both reference implementations did their arithmetic in float16: BatchNormalization's training-mode variance squares the input and overflows the float16 range above ~256 (output_var came out as `inf` with the true value still representable, and the output collapsed to zeros), and LpNormalization's power-2 norm overflowed the same way, returning `[0, 0, 0]` instead of `[0.42, 0.57, 0.71]`. Both now compute in float32 for float16/bfloat16 inputs — the same fix the maintainers shipped for InstanceNormalization, LRN, LogSoftmax and SoftmaxCrossEntropyLoss days earlier; found by sweeping the remaining normalization/reduction ops for the class | 🟢 Open · in review |
| [#8786 — compute LpPool in float32 for float16/bfloat16](https://github.com/onnx/onnx/pull/8786) | The pooling sibling of #8772: LpPool raised the input to the power `p` in the input dtype, so float16 windows containing values above 256 pooled to `inf` while the true L2 norms were representable. GlobalLpPool already computes in log space and needed nothing; found while sweeping the rest of the pool family | 🟢 Open · in review |

<a name="onnx"></a>

## <img src="https://github.com/onnx.png" width="24" alt="ONNX"> ONNX (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8758 — accept omitted optional inputs in Dropout](https://github.com/onnx/onnx/pull/8758) | The reference implementation picked `Dropout`'s optional inputs by position count, but the evaluator hands over an omitted optional input as `None` instead of dropping it — so a training-mode model that leaves out `ratio` (legal per spec; the default is 0.5) crashed with a `TypeError`, and every opset-12 node carrying the `training_mode` attribute failed before the implementation even ran, because that attribute arrived as a keyword the function never declared. Found with a differential sweep that omits each optional input from all 1,876 node tests and runs the result through the reference evaluator — `Dropout` was the only op whose crash wasn't a deliberate validation guard | 🟢 Open · maintainer-approved (justinchuby) · CI awaiting first-time workflow approval |
| [#8760 — round QLinearConv before adding y_zero_point](https://github.com/onnx/onnx/pull/8760) | The reference quantized the accumulator with ties-to-even rounding *after* adding the zero point, while the spec rounds the quotient first — the orders disagree whenever the quotient is a half-integer and the zero point is odd (quotient 0.5 with zero point 1: spec 1, reference 2). Found by mining the merged QLinearMatMul fix (#8700) for unfixed siblings — `QLinearConv` was the one remaining op in the class | 🟢 Open · in review · CI awaiting first-time workflow approval |

<a name="pipx"></a>

## <img src="https://github.com/pypa.png" width="24" alt="pipx"> pipx

| Pull request | What it fixes | Status |
|---|---|---|
| [#2423 — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423) | `pipx repair` reported environments whose `pipx_metadata.json` a killed install lost as "healthy" (exit 0), even though the project's own #2234 hardening makes `pipx reinstall` and `pipx reinstall-all` refuse them — the repair flow could only reach that refusal through a broken interpreter, so a still-running one silenced it and a user following `pipx list`'s fix advice got a silent no-op — fixes [#2422](https://github.com/pypa/pipx/issues/2422), self-found by auditing the killed-install hardening series for the command its changelog promised but never wired | ✅ Merged — approved by the maintainer within the hour |
| [#2431 — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431) | every repeat `pipx ensurepath` run claimed "all pipx binary directories have been appended to PATH" when nothing was appended — the directories were already in PATH, so the summary reported a change that did not happen and pointed users at `--force`; reworded to report the true state and the `--force`/`--prepend` way to re-add, with the summary checking every directory before making the claim — fixes [#2430](https://github.com/pypa/pipx/issues/2430) | ✅ Merged — lead maintainer merged with the `bug` label, 27 checks green |

<a name="wheel"></a>

## <img src="https://github.com/pypa.png" width="24" alt="wheel"> wheel

| Pull request | What it fixes | Status |
|---|---|---|
| [#719 — don't leave the .dist-info directory renamed when 'wheel pack --local-version' fails](https://github.com/pypa/wheel/pull/719) | The rename to the new name-version `.dist-info` directory ran before anything else could fail, so a missing `METADATA` or `WHEEL` file, a `WHEEL` file without tags, or any write error left the unpacked directory under a name no wheel was ever produced for — everything that can fail before the rename now runs before it, and a failure after it puts the directory back — fixes [#713](https://github.com/pypa/wheel/issues/713), four regression tests each verified to fail on the unfixed code | ⚪ Withdrawn — an earlier fix ([#714](https://github.com/pypa/wheel/pull/714)) existed; closed in its favor with the guard + tests offered as a contribution there |

<a name="pytorch"></a>

## <img src="https://github.com/meta-pytorch.png" width="24" alt="BoTorch"> BoTorch

| Pull request | What it fixes | Status |
|---|---|---|
| [#3550 — preserve float64 precision of a Python-float best_f](https://github.com/meta-pytorch/botorch/pull/3550) | The analytic acquisition functions document `best_f` as "either a scalar or a `b`-dim Tensor", but the scalar form was rounded through the default dtype at construction while the Tensor form kept full precision — and Expected Improvement is exponentially sensitive to `best_f`, so with a double model and a large-magnitude incumbent the two forms disagreed by 137 orders of magnitude (EI `7.07e-02` vs `1.51e-139`) — fixes [#3549](https://github.com/meta-pytorch/botorch/issues/3549), self-found by mining the just-merged `make_scipy_bounds` precision fix (#3542) for the same Python-scalar-through-default-dtype class across the acquisition package | 🟢 Open · all local tests green incl. new regression test · Meta CLA signature pending |

<a name="pytorch-core"></a>

## <img src="https://github.com/pytorch.png" width="24" alt="PyTorch"> PyTorch

| Pull request | What it fixes | Status |
|---|---|---|
| [#203846 — make inductor's index_reduce validation match eager](https://github.com/pytorch/pytorch/pull/203846) | Inductor's own decomposition of `aten.index_reduce` checked devices but skipped the shape/dtype checks eager applies, so a scalar `self` with a 1-dim `source` broadcast through the mean path and silently returned `3.5` where eager raises "source tensor shape must match self tensor shape" — fixes [#202938](https://github.com/pytorch/pytorch/issues/202938), reproduced locally through the full raw/eager/aot_eager/inductor matrix after setting up MSVC + Windows SDK for torch.compile on this machine, fix verified on the nightly wheel with both the new regression test and the existing index_reduce test passing | 🟢 Open · ready for review · CLA signature pending |
| [#203631 — validate SGD's dampening range](https://github.com/pytorch/pytorch/issues/203631) | SGD checks `lr`, `momentum` and `weight_decay` but not `dampening`, so values outside [0, 1] are silently accepted and the momentum buffer extrapolates instead of interpolating — a buffer that swings negative or grows without bound, with no error, on both the foreach and single-tensor paths; every sibling optimizer already validates its range-bounded parameters (Adadelta's `rho`, RMSprop's `alpha`, Adagrad's `lr_decay`, ASGD's `lambd`/`alpha`) — self-found by comparing each optimizer's validators against the parameters its update math actually consumes | 🟡 Issue filed · bot-triaged · awaiting `actionable` label · PR queued behind it (PyTorch requires the label before a PR) |
| [#203849 — inductor's index_add has the same missing shape validation](https://github.com/pytorch/pytorch/issues/203849) | The sibling decomposition in the same file skips eager's shape check too: a scalar `self` with a 1-dim `source` silently returns `7.0` where eager raises — found by probing the next op in the family while the index_reduce fix was in CI | 🟡 Issue filed · awaiting `actionable` label · PR queued behind it |

<a name="cibuildwheel"></a>

## <img src="https://github.com/pypa.png" width="24" alt="cibuildwheel"> cibuildwheel

| Pull request | What it fixes | Status |
|---|---|---|
| [#3038 — reject unsupported bash parameter expansions in environment values](https://github.com/pypa/cibuildwheel/pull/3038) | `${VAR:-default}`-style parameter nodes in `CIBW_ENVIRONMENT` expanded silently to a wrong value instead of failing — unsupported expansions fell through and escaped-`$` words expanded at the wrong position; the evaluator now rejects non-plain-name parameters loudly with the module's standard unsupported-construct error, single-char bash specials keep legacy behavior, +2 regression tests — full unit suite 937 passed / 70 skipped / 3 xfailed, green | 🟢 Open · all 7 CI checks green · 937-test unit suite green · awaiting review |

| Bug report | What it documents | Status |
|---|---|---|
| [#3039 — environment values with an escaped dollar followed by the same variable expand at the wrong position](https://github.com/pypa/cibuildwheel/issues/3039) | `\$X$X` in one word expands to `y$X` where bash produces `$Xy` — the leftmost-occurrence `replace()` targets the part's text, not its position; filed with a bash ground-truth probe table, the root cause, and why the naive fixes (rfind) break the mirrored case | 🟡 Filed — fix directions documented |

<a name="argocd"></a>

## <img src="https://github.com/argoproj.png" width="24" alt="Argo"> Argo CD (CNCF)

| Pull request | What it fixes | Status |
|---|---|---|
| [#30892 — format float64 generator params as plain decimals for selector matching](https://github.com/argoproj/argo-cd/pull/30892) | `flattenParameters` formats generator parameter values with `fmt.Sprintf("%v", ...)`, and float64 renders via `%g` — JSON/YAML numbers ≥ 1e6 or < 1e-4 become scientific notation (`1.762e+09`), so a post-generator selector comparing `n=1762000000` silently never matches; now formatted in plain decimal notation — fixes [#30891](https://github.com/argoproj/argo-cd/issues/30891), self-found with a probe: `float64(1762000000)` → `"1.762e+09"`, selector match `false` | 🟢 Open · 43/43 checks green across two full CI cycles · CodeRabbit-clean · maintainer review points addressed same-day · awaiting approval |

---

*This page is the running index — it updates as pull requests move through review and merge, in the order the work happened.*

**Open to internships and entry-level backend / infrastructure roles** · [GitHub](https://github.com/AP24110011695) · [LinkedIn](https://www.linkedin.com/in/ayush-kumar-saha-5126b6379)
