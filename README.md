# Open Source Contributions — Ayush (AP24110011695)

All of my open source work in one place — every pull request, bug report and fix below is real and linked.

[Merged](#merged) · [crewAI](#crewai) · [fastmcp](#fastmcp) · [layer5](#layer5) · [mem0](#mem0) · [reflex](#reflex) · [agno](#agno) · [ollama-python](#ollama) · [Powertools](#powertools) · [Actual Budget](#actual) · [WeatherGenerator](#weathergen) · [pypdf](#pypdf) · [NiceGUI](#nicegui) · [Iceberg](#iceberg) · [Airflow](#airflow)

🟢 in review · 🟡 waiting on a maintainer · 🔒 gated on triage · ⚪ closed

---

## How I work

- I find most bugs myself by reading the code — the issues behind them are mine too, not ones I picked off a shelf.
- Every fix starts with a small failing test on the project's own `main`, to prove the bug is real. Then the fix, and the same test passing.
- I read each project's contribution rules before opening anything — sign-offs, issue gates, PR templates — so nothing I send breaks their flow.
- Every pull request explains the root cause and links the issue it fixes.
- When a reviewer leaves feedback, I fix it the same day and reply with the commit that addresses it.
- Tests mock real external services — never the code under test.

---

## Merged

| Pull request | What it fixes | Project |
|---|---|---|
| [#677 — reject whitespace-only API key names](https://github.com/nikhilb2/simple_invoicing/pull/677) | `POST /api/api-keys/` saved a name of only spaces as an empty string; now returns 422 — merged within the hour of opening | simple_invoicing |
| [#678 — reject blank units and unknown statuses on product update](https://github.com/nikhilb2/simple_invoicing/pull/678) | Product updates silently accepted a blank unit and any status string; now reuses the create-path unit validation and bounds status to active/inactive with 422s — merged the same day, after addressing a maintainer change request with the requested API-level test | simple_invoicing |
| [#130 — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130) | `rai assess <model-ref>` crashed with raw Python tracebacks for malformed refs, missing modules, and missing classes — now a clean input error, while a valid model's own factory or constructor failures keep their original exception and traceback — merged after a full human review cycle: changes requested on the exception boundary, corrected to the maintainer's spec, approved | rai-toolkit (Weights & Biases) |

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
| [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) | JSON-pointer-escaped schema names broke schema extraction — fixes [#6034](https://github.com/PrefectHQ/fastmcp/issues/6034) | 🟡 Open · awaiting maintainer issue assignment |
| [#6185 — keep `tools/list` working when a root `$ref` resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | Whole-server tools listing crashed on valid schemas — fixes [#6125](https://github.com/PrefectHQ/fastmcp/issues/6125) | 🟡 Open · awaiting maintainer issue assignment |
| [#6187 — support non-identifier variables in URI templates](https://github.com/PrefectHQ/fastmcp/pull/6187) | `{$top}`-style template variables never matched or forwarded; Unicode word characters that identifiers reject also disabled templates | 🟡 Open · two bot-review rounds, findings fixed same day · awaiting maintainer issue assignment |
| [#6188 — keep result hydration faithful for union coercions](https://github.com/PrefectHQ/fastmcp/pull/6188) | `0 → False`-style coercions silently replaced typed results; final guard also preserves schema-intended `format: json` decodes and rejects precision-losing timestamp truncation | 🟡 Open · two bot-review rounds, findings fixed same day · awaiting maintainer issue assignment |
| [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) | Tags added by a server's `tools` config were invisible to `include_tags`/`exclude_tags` on single-server MCPConfigs — fixes [#6196](https://github.com/PrefectHQ/fastmcp/issues/6196) | 🟡 Open · triage bot found no defects, verified fail→pass |

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
| [#7704 — `ln()` creates the link at dest pointing to src](https://github.com/reflex-dev/reflex/pull/7704) | The public path helper did the exact opposite of `ln -s` semantics, and `overwrite=True` never worked for files | 🟡 Open · passed three rounds of automated review · awaiting human review |
| [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) | The array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds — follow-up to #7691 | 🟡 Open · awaiting review |

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
| [#4353 — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353) | Two code paths (font listing and inline-image color-space lookup) still crashed with `TypeError` when `/Resources` was not a dictionary — the same robustness class fixed twice elsewhere in the codebase — fixes [#4352](https://github.com/py-pdf/pypdf/issues/4352), a self-found bug located by mining that repeated fix pattern | 🟢 Open · in review |

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

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache OpenDAL (data access layer)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8484 — trim whitespace in `normalize_root`](https://github.com/apache/opendal/pull/8484) | `normalize_root`'s own documented rules say whitespace is trimmed (identical wording to `normalize_path`, which trims and is pinned-tested), but the code never did — a root configured as `" my-dir "` became `"/ my-dir /"` and every object path under the backend silently carried the spaces | 🟢 Open · in review |

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Pulsar (pub-sub messaging)

| Pull request | What it fixes | Status |
|---|---|---|
| [#27375 — handle empty values in FieldParser converters and setEmptyValue](https://github.com/apache/pulsar/pull/27375) | `stringToLong("")`/`stringToFloat("")` crashed with `NumberFormatException` while the Integer/Double siblings return `null` (their guard was never added to these two), and `setEmptyValue`'s String check compared the type object's class to `String.class` — always false — so blank values left stale Strings instead of clearing them — fixes [#27374](https://github.com/apache/pulsar/issues/27374), self-found by reading the config-parsing utilities against their own sibling patterns | 🟢 Open · in review |

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Superset (data visualization)

| Pull request | What it fixes | Status |
|---|---|---|
| [#46040 — reject deeply nested date expressions with a parse error](https://github.com/apache/superset/pull/46040) | `datetime_eval` converts only `ParseException`, but the date-expression grammar recurses once per nesting level — a pasted ~500-character time range (60–80 nested `dateadd(` calls, measured on master) exhausted the interpreter stack and hit the chart-data and Jinja paths as an unhandled `RecursionError` (500) instead of the parse error every other malformed expression produces — fixes [#46039](https://github.com/apache/superset/issues/46039), self-found by fix-commit mining the freshly-fixed date-parser area | 🟢 Open · in review |

---

*This page is the running index — it updates as pull requests move through review and merge, in the order the work happened.*
