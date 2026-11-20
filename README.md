# Open Source Contributions — Ayush (AP24110011695)

I find and fix real bugs in production open-source projects — by reading the code, writing the failing test first, and shipping small, reviewed changes. Everything on this page is real and linked.

**29 pull requests merged** · **32 projects** · **19 code reviews of other contributors' PRs (12 approvals — 7 of the reviewed PRs have since merged)** — across PyPA, Apache, CNCF, the Linux Foundation, Meta, AWS, ECMWF and Weights & Biases

Languages & domains: Python · Go · Java · Rust · C/C++ · TypeScript — CLI tooling, PDF parsing, ML infrastructure, data formats, CI & packaging, monitoring, pub-sub messaging

Status legend: ✅ merged / approved · 🟢 open, in review · 🟡 waiting on a maintainer · 🔒 closed by a triage bot, auto-reopens on signal · ⚪ closed / withdrawn

---

## Highlights

**[pipx (PyPA) — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423)**
`pipx repair` reported environments whose metadata a killed install had lost as "healthy" (exit 0), while the project's own reinstall flow refuses them — so a user following `pipx list`'s fix advice got a silent no-op. Self-found by auditing the killed-install hardening series for the command its changelog promised but never wired. **Approved by the maintainer within the hour, merged the same night.**

**[pipx (PyPA) — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431)**
Every repeat `pipx ensurepath` run claimed it had appended directories to PATH when they were already there — reporting a change that never happened and pointing users at `--force` for nothing. **Merged by the lead maintainer with the `bug` label, 27 checks green.**

**[pypdf — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353)**
Two code paths still crashed with `TypeError` on malformed PDFs — the same robustness class the project had already fixed twice elsewhere; located by mining that repeated fix pattern for unfixed siblings. **Merged after the full review cycle** — coverage requested and covered, five maintainer suggestions applied, two of them test-proven corrections to the suggestions themselves.

**[AWS Lambda Powertools — tolerate a malformed parameters cache-TTL environment variable](https://github.com/aws-powertools/powertools-lambda-python/pull/8757)**
An empty or non-integer `POWERTOOLS_PARAMETERS_MAX_AGE` crashed all 12 parameters entry points before any AWS call; now warns and falls back to the documented default. **Merged after the maintainer ran the whole parameters suite himself** — released in [v3.41.0](https://github.com/aws-powertools/powertools-lambda-python/releases/tag/v3.41.0), credited by name in the release notes.

**[fastmcp — keep tools/list working when a root $ref resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185)**
A valid JSON Schema (`$ref` resolving to `true`/`false`) crashed whole-server tool listing during client init. **Merged with two sibling fixes in the same batch** — URI-template variables and tag-filter ordering — four merges in one day.

**[Zephyr RTOS — unlock interrupts on invalid pin configurations](https://github.com/zephyrproject-rtos/zephyr/pull/124927)**
Two GPIO drivers returned `-ENOTSUP` from their configure callbacks with interrupts still locked — freezing the system on malformed pin configs. Found by scanning every `irq_lock()` error path in `drivers/` after the same freeze bug was fixed in two DMA drivers a day apart. **First contribution to the project — approved by two maintainers, merged by Anas Nashif, backport to the stable branch requested.**

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

## Merged pull requests

One row per project — every merge is a clickable link. Details for each merge are in the project sections below.

| Project | Merged pull requests |
|---|---|
| [**simple_invoicing**](https://github.com/nikhilb2/simple_invoicing) | [#677 — reject whitespace-only API key names](https://github.com/nikhilb2/simple_invoicing/pull/677) · [#678 — reject blank units and unknown statuses on product update](https://github.com/nikhilb2/simple_invoicing/pull/678) |
| [**rai-toolkit**](https://github.com/wandb/rai-toolkit) (Weights & Biases) | [#130 — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130) |
| [**pipx**](https://github.com/pypa/pipx) (PyPA) | [#2423 — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423) · [#2431 — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431) · [#2446 — skip prerelease builds in the standalone-Python version index](https://github.com/pypa/pipx/pull/2446) |
| [**reflex**](https://github.com/reflex-dev/reflex) | [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) |
| [**fastmcp**](https://github.com/PrefectHQ/fastmcp) | [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) · [#6185 — keep tools/list working when a root $ref resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) · [#6187 — make resource templates for non-identifier path parameters readable](https://github.com/PrefectHQ/fastmcp/pull/6187) · [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) |
| [**pypdf**](https://github.com/py-pdf/pypdf) | [#4353 — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353) |
| [**osquery**](https://github.com/osquery/osquery) (Linux Foundation) | [#9283 — check netlink attribute payload lengths before typed reads in routes](https://github.com/osquery/osquery/pull/9283) · [#9322 — guard the prometheus_targets config against malformed values](https://github.com/osquery/osquery/pull/9322) · [#9280 — reject truncated file-entry records in fileEntry instead of throwing](https://github.com/osquery/osquery/pull/9280) |
| [**Zephyr RTOS**](https://github.com/zephyrproject-rtos/zephyr) (Linux Foundation) | [#124927 — unlock interrupts on invalid pin configurations](https://github.com/zephyrproject-rtos/zephyr/pull/124927) · [#124961 — unlock interrupts on USB error paths](https://github.com/zephyrproject-rtos/zephyr/pull/124961) · [#125508 — avoid 64-bit divisions in TDK temperature conversions](https://github.com/zephyrproject-rtos/zephyr/pull/125508) · [#124962 — unlock interrupts on grant double-free](https://github.com/zephyrproject-rtos/zephyr/pull/124962) · [#125797 — reset the MQTT disconnect reason between sessions](https://github.com/zephyrproject-rtos/zephyr/pull/125797) · [#125909 — clear MQTT topic alias mappings on connection reset](https://github.com/zephyrproject-rtos/zephyr/pull/125909) · [#125667 — close the connection on unexpected packet types](https://github.com/zephyrproject-rtos/zephyr/pull/125667) |
| [**PyIceberg**](https://github.com/apache/iceberg-python) (Apache) | [#4285 — handle negative-scale Decimals in increment, decrement and truncate_decimal](https://github.com/apache/iceberg-python/pull/4285) · [#4287 — reject non-finite floats on conversion to Decimal](https://github.com/apache/iceberg-python/pull/4287) · [#4331 — order -0.0 below 0.0 in data file metrics bounds](https://github.com/apache/iceberg-python/pull/4331) |
| [**Powertools for AWS Lambda**](https://github.com/aws-powertools/powertools-lambda-python) (Python) | [#8757 — tolerate a malformed parameters cache-TTL environment variable](https://github.com/aws-powertools/powertools-lambda-python/pull/8757) |
| [**virtualenv**](https://github.com/pypa/virtualenv) (PyPA) | [#3528 — skip generated-file-link tests without symlinks](https://github.com/pypa/virtualenv/pull/3528) · [#3570 — drop yanked releases from the update log](https://github.com/pypa/virtualenv/pull/3570) |
| [**cibuildwheel**](https://github.com/pypa/cibuildwheel) (PyPA) | [#3049 — map unknown host machines to the graceful no-native-arch path](https://github.com/pypa/cibuildwheel/pull/3049) |

---

## Code reviews — other contributors' pull requests

I also review pull requests from other contributors. An approval from me means I checked out their branch, ran the tests, and reproduced the bug being fixed on the unfixed code first — not that the diff merely looked fine.

| Review | What I verified | Outcome |
|---|---|---|
| [#4289 — skip unknown nested fields when resolving Avro read schemas](https://github.com/apache/iceberg-python/pull/4289#pullrequestreview-5790634073) — PyIceberg | ran the PR's own test locally and probed all four type-mismatch guarantees (map-vs-string, list-vs-map, top-level and field-level) still raise | ✅ Approved — [merged](https://github.com/apache/iceberg-python/pull/4289) |
| [#4296 — read a file without avro.codec as uncompressed](https://github.com/apache/iceberg-python/pull/4296#pullrequestreview-5804767229) — PyIceberg | ran the new codec tests on the branch and reproduced the pre-fix failure (`Unsupported codec: gzip`) on the old code, then mapped every config-fallback site the one-line change touches | ✅ Approved — [merged](https://github.com/apache/iceberg-python/pull/4296) |
| [#4292 — apply every delete file when rewriting files for a partial delete](https://github.com/apache/iceberg-python/pull/4292#pullrequestreview-5807190431) — PyIceberg | a partial delete could resurrect deleted rows when filtered reads bounds-prune delete files — confirmed the fix's rationale, ran the new test across three catalog fixtures, reproduced the exact deleted-rows-returning failure on the unfixed code, and ran the 721-test behavior regression slice | ✅ Approved — [merged](https://github.com/apache/iceberg-python/pull/4292) |
| [#4333 — retry appends on catalogs that only expose the current snapshot](https://github.com/apache/iceberg-python/pull/4333#pullrequestreview-5850663772) — PyIceberg | traced the retry-guard class structure (the only new `base=None` case is intercepted before use), ran the full commit-retry suite (129 passed on branch), fail-first: 9 failed on main | ✅ Approved |
| [#4347 — check add_files duplicates against the target branch](https://github.com/apache/iceberg-python/pull/4347#pullrequestreview-5865010567) — PyIceberg | verified the dedup logic (snapshots by id, manifests by path, `snapshot_by_name(None)` safe), 12 passed on branch, fail-first: the 2 rejection tests failed on main | ✅ Approved |
| [#4529 — fail MonitorServiceTest if nothing throws](https://github.com/apache/hertzbeat/pull/4529#pullrequestreview-5805159800) — HertzBeat | read all 11 try/catch → assertThrows conversions, ran the test module locally (71/71 green), then did an independent mutation check: commenting out a real throw in the service made the new test fail — proving the old pattern would have passed silently | ✅ Approved |
| [#4526 — add the missing SSL parameter to HDFS NameNode/DataNode/YARN](https://github.com/apache/hertzbeat/pull/4526#pullrequestreview-5790679437) — HertzBeat | traced the diagnosis end-to-end (the placeholder survives substitution, so `Boolean.parseBoolean` always answers false), then scope-checked it: grepped all 40 templates using the SSL placeholder — the PR's 3 files are the complete set | 💬 Commented — confirmed the scope is complete |
| [#76629 — DAG-level on_failure_callback dropped on detached session errors](https://github.com/apache/airflow/pull/76629#pullrequestreview-5807222864) — Airflow | verified the exception-catch hierarchy statically (`PendingRollbackError`/`InvalidRequestError` both escape the `DetachedInstanceError`-only catch) and flagged a sibling path pruning entries the same way | 💬 Commented — same-class sibling flagged |
| [#2448 — preserve lock files through interrupts](https://github.com/pypa/pipx/pull/2448#pullrequestreview-5882404801) — pipx | verified the SIGINT/SIGTERM deferral semantics (backups survive rollback, deferred interrupt still reported), ran all 6 new tests, fail-first: 3 of 4 parametrized cases fail on main's source | ✅ Approved — [merged](https://github.com/pypa/pipx/pull/2448) |
| [#2450 — docs: what `environment --value` prints for unset variables](https://github.com/pypa/pipx/pull/2450#pullrequestreview-5865107238) — pipx | verified all four docs claims — the derived-vs-raw split against the source, ran `--value PIPX_GLOBAL_BIN_DIR` and `PIPX_HOME` live, and code-read the `--global` path | ✅ Approved — [merged](https://github.com/pypa/pipx/pull/2450) |
| [#2453 — resume Python downloads cut short of Content-Length](https://github.com/pypa/pipx/pull/2453#issuecomment-6836962614) — pipx | verified against main's resume loop: the length-shortfall raise covers silent short-reads, `IncompleteRead` routes through the transient retry + disk-resume, the post-assembly checksum makes wrong-resume impossible | 💬 Verified — support posted, [merged](https://github.com/pypa/pipx/pull/2453) |
| [#2462 — write pipx_shared.pth in the encoding the venv's Python reads](https://github.com/pypa/pipx/pull/2462#pullrequestreview-5928788452) — pipx | PEP-686 encoding mismatch — verified write side uses `locale.getencoding()` with a UTF-8 fallback, read side matches 3.12+ precedence, all call sites wired, 5 tests pass on branch | ✅ Approved — [merged](https://github.com/pypa/pipx/pull/2462) |
| [#2481 — continue upgrade when an environment or build fails](https://github.com/pypa/pipx/pull/2481#issuecomment-6995686563) — pipx | confirmed all three failure modes covered (per-env `PipxError` with the environment name + continue, the outcome.errors branch, per-build download failure with environment=None), regression-checked the no-op case (`succeeded=False` can't flip status to error), and confirmed cached-venvs staleness stays benign | 💬 Verified — support posted |
| [#3041 — expand variables at their own position in environment values](https://github.com/pypa/cibuildwheel/pull/3041#pullrequestreview-5865203063) — cibuildwheel | environment tests 18 passed + full unit suite 942 passed, fail-first: the 3 new tests fail with main's source swapped in — also fixes our filed [#3039](https://github.com/pypa/cibuildwheel/issues/3039) | 💬 Commented — fail-first verified (repo refuses APPROVE events from outside collaborators) |
| [#3042 — read environment assignments on every line](https://github.com/pypa/cibuildwheel/pull/3042#pullrequestreview-5882294947) — cibuildwheel | multi-line `CIBW_ENVIRONMENT` blocks dropped every line after the first — verified the parse guard, ran the full suite (936 passed), fail-first on main; raised the comment-handling question | 💬 Commented — fail-first verified (same repo policy) |
| [#3543 — correct marginal densities and entropy constant in batch MC JES](https://github.com/meta-pytorch/botorch/pull/3543#pullrequestreview-5897103393) — BoTorch | math-verified both bugs (missing entropy constant copies, joint density broadcast into marginal terms); new additivity regression passes on branch and fails on main with abs error 2.6165 | ✅ Approved |
| [#3546 — compute Gaussian mixture variance from centered means](https://github.com/meta-pytorch/botorch/pull/3546#pullrequestreview-5897205288) — BoTorch | catastrophic-cancellation fix (`E[X²]−E[X]²` → `var(correction=0)`): float32 subtests fail on main, pass on branch — exactly the claimed pattern | ✅ Approved |
| [#3563 — fix dtype and batch shape of out-of-bounds TruncatedMultivariateNormal.log_prob](https://github.com/meta-pytorch/botorch/pull/3563#pullrequestreview-5928722679) — BoTorch | the early return built a default-float32 tensor and dropped the candidate dim — full probability file 5 passed on branch, fails on main with the exact dtype-mismatch assertion | ✅ Approved |
| [#3393 — shared-parameter batched fitting + timeouts in the fit machinery](https://github.com/meta-pytorch/botorch/pull/3393) — BoTorch | probed `maxiter=0` on the fit path: L-BFGS-B still performs one full iteration (the Fortran budget check runs after the step — upstream scipy behavior, isolated empirically) and flagged that the same after-the-step shape may affect the timeout callback's last iteration — posted as verified review-input on the in-flight rework | 💬 Review input posted — verified finding |

---

## The full log — by project

**PyPA** — [cibuildwheel](#cibuildwheel) · [pipx](#pipx) · [virtualenv](#virtualenv) · [wheel](#wheel)

**Apache** — [Airflow](#airflow) · [HertzBeat](#hertzbeat) · [OpenDAL](#opendal) · [PyIceberg](#iceberg) · [Pulsar](#pulsar) · [Superset](#superset)

**CNCF** — [Argo CD](#argocd) · [Dapr](#dapr)

**Linux Foundation** — [ONNX](#onnx) · [osquery](#osquery) · [Zephyr RTOS](#zephyr)

**Meta** — [BoTorch](#botorch) · [PyTorch](#pytorch)

**More** — [Actual Budget](#actual) · [agno](#agno) · [AWS Amplify](#aws-amplify) · [crewAI](#crewai) · [ECMWF WeatherGenerator](#weathergen) · [fastmcp](#fastmcp) · [layer5](#layer5) · [mem0](#mem0) · [NiceGUI](#nicegui) · [ollama-python](#ollama) · [pypdf](#pypdf) · [Powertools for AWS](#powertools) · [rai-toolkit](#rai-toolkit) · [reflex](#reflex) · [simple_invoicing](#simple-invoicing)

---

<a name="cibuildwheel"></a>

## <img src="https://github.com/pypa.png" width="24" alt="cibuildwheel"> cibuildwheel (PyPA)

| Pull request | What it fixes | Status |
|---|---|---|
| [#3038 — reject unsupported bash parameter expansions in environment values](https://github.com/pypa/cibuildwheel/pull/3038) | `${VAR:-default}`-style parameter nodes in `CIBW_ENVIRONMENT` expanded silently to a wrong value instead of failing — unsupported expansions fell through and escaped-`$` words expanded at the wrong position; the evaluator now rejects non-plain-name parameters loudly (single-char bash specials keep legacy behavior) | 🟢 Open · **approved by agriyakhetarpal** ("Makes sense to me!") — henryiii pushed a regex-precompile refactor onto the branch (maintainer-owned head) · merge blocked only by the repo-wide linux_313 runner failure (our [#3057](https://github.com/pypa/cibuildwheel/pull/3057) fixes it) |
| [#3043 — reject unknown option names in overrides sections](https://github.com/pypa/cibuildwheel/pull/3043) | unknown keys under an `overrides` section were silently ignored (the global `--platform` path validates, the overrides path never did); scope deliberately limited to known-name validation — enforcing the docs' disallowed-options rules would be a behavior change, flagged for maintainers | 🟢 Open · maintainer-endorsed approach + both hardening asks adopted · awaiting mayeut's re-review after the single-commit rebase |
| [#3044 — raise a clean error for empty build-frontend and container-engine values](https://github.com/pypa/cibuildwheel/pull/3044) | an empty `build-frontend`/`container-engine` config value crashed with a raw KeyError/AttributeError deep in the evaluator instead of the module's standard unsupported-construct error — both `from_config_string` sites now raise a named ValueError that the callers' existing wrappers turn into clean ConfigurationErrors | 🟢 Open · **approved by agriyakhetarpal** — henryiii rebased it (maintainer-owned head) · merge blocked only by the linux_313 runner failure (our [#3057](https://github.com/pypa/cibuildwheel/pull/3057) fixes it) |
| [#3049 — map unknown host machines to the graceful no-native-arch path](https://github.com/pypa/cibuildwheel/pull/3049) | `native_arch` crashed with a raw ValueError on unknown host machines (e.g. loongarch64) instead of returning the designed None → clean nothing-to-build handling; pyodide always returns wasm32 regardless of host, ios compares the raw machine string | ✅ **MERGED** by henryiii (approvals: henryiii + agriyakhetarpal) — the first cibuildwheel merge, after the community reviewer's regression finding was fixed (host-independent paths can't touch the host machine); issue #3048 closed as completed via it |
| [#3057 — free the Azure hosted runner disk before the Linux test suite](https://github.com/pypa/cibuildwheel/pull/3057) | the repo-wide linux_313 job failed on main and every approved PR for days — root-caused through the public Azure DevOps REST timeline: 95% disk used before the suite, then `docker create --pull=always` for the manylinux container dies with `no space left on device` (capacity, not flake — reruns don't fix). The cleanup step removes dotnet/Android/GHC/CodeQL hosted-image caches + prunes docker state; **proven on the PR's own Azure build: disk 95% → 48%, linux_313 PASSED** — henryiii reviewed same-day (only ask: drop the comment block, applied) | 🟢 Open · **end-to-end proven** · merging it unblocks the approved #3038/#3043/#3044 queue |

| Bug report | What it documents | Status |
|---|---|---|
| [#3039 — environment values with an escaped dollar followed by the same variable expand at the wrong position](https://github.com/pypa/cibuildwheel/issues/3039) | `\$X$X` in one word expands to `y$X` where bash produces `$Xy` — the leftmost-occurrence `replace()` targets the part's text, not its position; filed with a bash ground-truth probe table | 🟡 Filed — the lead maintainer raised the positional-mapping fix upstream in bashlex ([#102](https://github.com/idank/bashlex/pull/102)); community PR [#3041](https://github.com/pypa/cibuildwheel/pull/3041) (reviewed by us) holds until it lands; our staged fix parked as documented backup |
| [#3046 — overrides silently ignore global-only options](https://github.com/pypa/cibuildwheel/issues/3046) | `build`/`skip`/`test-skip`/`enable` under an overrides section are accepted and never applied — the docs promise they "cannot be set in an overrides section" but nothing enforces it | 🟡 Filed — awaiting maintainer decision (enforcement = behavior change) |
| [#3048 — unknown host machine crashes native_arch with a raw ValueError](https://github.com/pypa/cibuildwheel/issues/3048) | hosts like loongarch64 hit an unhandled machine string — filed with the crash trace | ⚪ Closed — completed via our merged [#3049](https://github.com/pypa/cibuildwheel/pull/3049) |
| [#3058 — linux_313 test job fails with `no space left on device` on Azure hosted runners](https://github.com/pypa/cibuildwheel/issues/3058) | diagnostic filed with the full evidence chain (Azure build timeline + task log + failure window: green through 11-17, consistently failing since, reruns don't fix) | 🟡 Filed — fix open as [#3057](https://github.com/pypa/cibuildwheel/pull/3057) |

| Bug report | What it documents | Status |
|---|---|---|
| [#3039 — environment values with an escaped dollar followed by the same variable expand at the wrong position](https://github.com/pypa/cibuildwheel/issues/3039) | `\$X$X` in one word expands to `y$X` where bash produces `$Xy` — the leftmost-occurrence `replace()` targets the part's text, not its position; filed with a bash ground-truth probe table | 🟡 Filed — the lead maintainer raised the positional-mapping fix upstream in bashlex ([#102](https://github.com/idank/bashlex/pull/102)); community PR [#3041](https://github.com/pypa/cibuildwheel/pull/3041) (reviewed by us) holds until it lands; our staged fix parked as documented backup |
| [#3046 — overrides silently ignore global-only options](https://github.com/pypa/cibuildwheel/issues/3046) | `build`/`skip`/`test-skip`/`enable` under an overrides section are accepted and never applied — the docs promise they "cannot be set in an overrides section" but nothing enforces it | 🟡 Filed — awaiting maintainer decision (enforcement = behavior change) |
| [#3048 — unknown host machine crashes native_arch with a raw ValueError](https://github.com/pypa/cibuildwheel/issues/3048) | hosts like loongarch64 hit an unhandled machine string — filed with the crash trace | ⚪ Closed — completed via our merged [#3049](https://github.com/pypa/cibuildwheel/pull/3049) |

<a name="pipx"></a>

## <img src="https://github.com/pypa.png" width="24" alt="pipx"> pipx (PyPA)

| Pull request | What it fixes | Status |
|---|---|---|
| [#2423 — refuse environments that lost their record](https://github.com/pypa/pipx/pull/2423) | `pipx repair` reported environments whose `pipx_metadata.json` a killed install lost as "healthy" (exit 0), even though the project's own #2234 hardening makes `pipx reinstall` refuse them — the repair flow could only reach that refusal through a broken interpreter, so a still-running one silenced it and a user following `pipx list`'s fix advice got a silent no-op — fixes [#2422](https://github.com/pypa/pipx/issues/2422), self-found by auditing the killed-install hardening series for the command its changelog promised but never wired | ✅ Merged — approved by the maintainer within the hour |
| [#2431 — report existing PATH entries accurately](https://github.com/pypa/pipx/pull/2431) | every repeat `pipx ensurepath` run claimed "all pipx binary directories have been appended to PATH" when nothing was appended — the directories were already in PATH, so the summary reported a change that did not happen and pointed users at `--force`; reworded to report the true state, with the summary checking every directory before making the claim — fixes [#2430](https://github.com/pypa/pipx/issues/2430) | ✅ Merged — lead maintainer merged with the `bug` label, 27 checks green |
| [#2446 — skip prerelease builds in the standalone-Python version index](https://github.com/pypa/pipx/pull/2446) | the version match stopped before a prerelease suffix, so all 195 `cpython-3.16.0a1` assets in the current python-build-standalone release aliased under the stable `3.16.0` key and `--fetch-python` downloaded an alpha while recording it as the final 3.16.0 — prerelease assets are now skipped, so a version with no final build fails loudly instead — fixes [#2445](https://github.com/pypa/pipx/issues/2445), found live against the release index, fail-first regression test included | ✅ Merged — maintainer refactored the match to read the tag once at merge, closed the issue as completed |

<a name="virtualenv"></a>

## <img src="https://github.com/pypa.png" width="24" alt="virtualenv"> virtualenv (PyPA)

| Pull request | What it fixes | Status |
|---|---|---|
| [#3528 — skip generated-file-link tests without symlinks](https://github.com/pypa/virtualenv/pull/3528) | the generated-file-links test suite created symlinks directly, so every Windows contributor without Developer Mode saw 20 failures (`WinError 1314`) no change of theirs could fix — the suite now skips via the repo's own `fs_supports_symlink` probe, the idiom two other test files already used | ✅ Merged — maintainer merged main in and aligned the skip reason at merge |
| [#3570 — drop yanked releases from the update log](https://github.com/pypa/virtualenv/pull/3570) | our verified order-dependence finding ([#3569](https://github.com/pypa/virtualenv/issues/3569), first test coverage `_select_version` ever had) opened as a sort-fix branch — the lead maintainer then took the branch over, diagnosed **yanked releases** as the real-world trigger that lets a lower version land above a newer one, and reworked it in place into a yank-detection subsystem (`index.py` reading PyPI yank status + drop-at-update-start); verified his rework locally (148 tests green) and posted the verification reply before merge | ✅ **Merged** — our PR number, the maintainer's rework inside it; issue #3569 closed as completed |

| Bug report | What it documents | Status |
|---|---|---|
| [#3569 — periodic update selection depended on the update log's insertion order](https://github.com/pypa/virtualenv/issues/3569) | `_select_version` grouped the update log assuming newest-first order, but successive updates interleave minors — a patch of an older minor downloaded by a later update landed before the newer minor's entry, splitting its group and letting an older version win the seed pick even past every grace period; verified live on main with a probe | ⚪ Closed — completed via [#3570](https://github.com/pypa/virtualenv/pull/3570) (our PR, reworked by the maintainer into the yank-detection fix) |

<a name="wheel"></a>

## <img src="https://github.com/pypa.png" width="24" alt="wheel"> wheel (PyPA)

| Pull request | What it fixes | Status |
|---|---|---|
| [#719 — don't leave the .dist-info directory renamed when 'wheel pack --local-version' fails](https://github.com/pypa/wheel/pull/719) | the rename to the new name-version `.dist-info` directory ran before anything else could fail, so a missing `METADATA` or `WHEEL` file, or any write error, left the unpacked directory under a name no wheel was ever produced for — everything that can fail before the rename now runs before it, and a failure after it puts the directory back — fixes [#713](https://github.com/pypa/wheel/issues/713), four regression tests each verified to fail on the unfixed code | ⚪ Withdrawn — an earlier fix ([#714](https://github.com/pypa/wheel/pull/714)) existed; closed in its favor with the guard + tests offered as a contribution there |

<a name="airflow"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Airflow (Task SDK)

| Pull request | What it fixes | Status |
|---|---|---|
| [#76481 — Fix `SecretCache` export in `airflow.sdk`](https://github.com/apache/airflow/pull/76481) | `SecretCache` resolved at runtime through the lazy-import map but was missing from `__all__` and the TYPE_CHECKING re-exports, so type checkers flagged every import — including seven inside Airflow core itself | ⚪ Closed after review — a contributor's main-branch verification showed the exclusion is deliberate (two named test exemptions + the type-checker stub already exporting it), withdrawn with thanks |
| [#76486 — Add `__dir__` to `airflow.sdk` so `dir()` exposes the lazy public API](https://github.com/apache/airflow/pull/76486) | the module resolved its 105-name public API through `__getattr__` alone, so `dir()` — what IDEs, REPLs and tooling discover — hid the entire surface until each name was touched; PEP 562 recommends pairing `__getattr__` with a `__dir__` | 🟢 Open · in review — rebased standalone after #76481 closed (the two fixes are independent) |
| [#76869 — Add `__dir__` to the airflow package root so dir() exposes lazy imports](https://github.com/apache/airflow/pull/76869) | the same PEP 562 gap one level up: the core `airflow` package root also resolved lazy imports through `__getattr__` alone, hiding them from `dir()` | 🟢 Open · in review |
| [#76935 — Fix `XComArg.zip()` and `concat()` when the upstream XCom is a dict](https://github.com/apache/airflow/pull/76935) | `resolve()` says dicts are valid for both, but only `map()` knew the convention since #75022 — zipping a dict upstream silently produced tuples filled with the raw `NOTSET` sentinel object (or key-lookup values on int-keyed dicts), and `concat()` yielded bare keys; both now emit `(key, value)` tuples — proven live on main before the fix; reviewer independently ran the tests on both trees, then prescribed the convert-once-in-resolve shape that took a 20k-key zip from 31s to 0.029s | 🟢 Open · in review, revision applied |
| [#77136 — resolve XCom backend loads only for keys that are stored through it](https://github.com/apache/airflow/pull/77136) | the get-side gate of the new language-SDK XCom backend never checked the key, so a runtime reading a `_link_` or skip-decision key sent the raw row value to the backend's load hook — a value that was never externalized; mirrors the set-side exclusions in all three get handlers — proven failing-first in the coordinator test harness | 🟢 Open · in review |

| Bug report | What it documents | Status |
|---|---|---|
| [#77346 — trigger-written XComs bypass the configured XCom backend](https://github.com/apache/airflow/issues/77346) | triggerer-written XComs land as raw rows while runtime writes are externalized refs — the GET gate resolves both through the backend's load hook, so strict backends break or mis-resolve on trigger-written keys; three design options laid out (backend-aware trigger path / provenance marker / documented tolerance), cross-referenced with #76212/#76596/#77136 | 🟡 Filed — needs a maintainer design decision |

<a name="hertzbeat"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache HertzBeat (real-time monitoring)

| Pull request | What it fixes | Status |
|---|---|---|
| [#4528 — recognize default-key ciphertext in `isCiphertext` under a custom key](https://github.com/apache/hertzbeat/pull/4528) | `isCiphertext` answered `false` for data encoded with the default secret key while a custom key was configured, while `aesDecode` decrypted the same payload via its default-key fallback — so callers deciding decrypt-vs-use-as-is treated real ciphertext as plaintext (three live call sites; a fourth already worked around it) — fixes [#4527](https://github.com/apache/hertzbeat/issues/4527), self-found by mining the project's fresh credential-hardening fixes for siblings | 🟢 Open · in review |
| [#4548 — stop jdbc connection property injection through database diagnostics](https://github.com/apache/hertzbeat/pull/4548) | the 2.0 gateway diagnostics service concatenated monitor-supplied host/port/database straight into a `jdbc:mysql://` url, so `db?allowLoadLocalInfile=true` injected arbitrary driver properties — exactly the attack class `JdbcUrlSafetyUtil` was built for in #4299, whose guard set the sibling `DatabaseToolsImpl` carries but this newer call site dropped — located by auditing every call site of the guard, regression tests verified failing-first | 🟢 Open · in review |

<a name="opendal"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache OpenDAL (data access layer)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8484 — trim whitespace in `normalize_root`](https://github.com/apache/opendal/pull/8484) | `normalize_root`'s own documented rules say whitespace is trimmed (identical wording to `normalize_path`, which trims and is pinned-tested), but the code never did — a root configured as `" my-dir "` became `"/ my-dir /"` and every object path under the backend silently carried the spaces | 🟢 Open · in review |

<a name="iceberg"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Iceberg (PyIceberg)

| Pull request | What it fixes | Status |
|---|---|---|
| [#4285 — handle negative-scale Decimals in increment, decrement and truncate_decimal](https://github.com/apache/iceberg-python/pull/4285) | three remaining call sites of a `Decimal` scale misread (`abs()` applied to the exponent) turned `1E+2` into `0.02` on increment — four orders of magnitude off; the same root cause was fixed elsewhere by #3997 — fixes [#4284](https://github.com/apache/iceberg-python/issues/4284), self-found by mining recently merged validation fixes for unfixed siblings | ✅ Merged by Fokko Driesprong — closed #4284 as completed |
| [#4287 — reject non-finite floats on conversion to Decimal](https://github.com/apache/iceberg-python/pull/4287) | an infinity float/double literal crashed `to(DecimalType)` with a bare `decimal.InvalidOperation` instead of the module's standard conversion error — fixes [#4286](https://github.com/apache/iceberg-python/issues/4286), self-found while auditing the conversion surfaces for unfixed siblings | ✅ Merged by Fokko Driesprong — closed #4286 as completed |
| [#4331 — order -0.0 below 0.0 in data file metrics bounds](https://github.com/apache/iceberg-python/pull/4331) | the parquet-metrics accumulator (`min(val, current)`) keeps whichever zero arrives last, so a late `-0.0` lowers an existing `+0.0` upper bound and a late `+0.0` raises an existing `-0.0` lower bound — the serialized bounds then order above a value present in the file; same class as the freshly merged #4324, flipped directions because the accumulator's argument order is flipped — proven failing-first on main for both arrival orders | ✅ Merged by Fokko Driesprong after his argument-order simplification round |
| [#4372 — convert float literals to wide decimal columns without InvalidOperation](https://github.com/apache/iceberg-python/pull/4372) | converting a float literal to a decimal column whose precision can't hold the value crashed with a bare `InvalidOperation` instead of the module's standard conversion error — fail-first proven for both overflow cases, the infinity/NaN contract from our merged #4287 preserved, with the >38-digit bind-time boundary documented as a non-blocking note | 🟢 Open · **approved by us + Fokko LGTM ("LGTM!")** — he independently ran the fail-first and echoed the dedup observation · merge-imminent |
| [#4412 — populate nan_value_counts when writing parquet files](https://github.com/apache/iceberg-python/pull/4412) | the parquet writer returned an empty `nan_value_counts` unconditionally — pyarrow's statistics API exposes no NaN count, so the writer now counts NaNs from the written table itself (`is_nan` sums, nulls excluded per the spec) and threads them through a new optional parameter; NaN-aware scan pruning had been silently dead for every pyiceberg-written table — fixes [#4396](https://github.com/apache/iceberg-python/issues/4396), filed by us | ⚪ Closed — superseded by merged #4401, which implemented the same fix from our issue the next morning (the issue stays open for the add_files follow-up) |
| [#4430 — render decimal human strings in plain notation](https://github.com/apache/iceberg-python/pull/4430) | decimal partition values rendered in scientific notation (`1.2E-7`) in the partitions inspect table's bound columns — the human-string helper had no Decimal handling while [#4420](https://github.com/apache/iceberg-python/pull/4420) established plain notation for decimal JSON values; extends that rule to the transform path — verified failing-first plus an end-to-end write + inspect probe | 🟢 Open · in review |

<a name="pulsar"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Pulsar (pub-sub messaging)

| Pull request | What it fixes | Status |
|---|---|---|
| [#27375 — handle empty values in FieldParser converters and setEmptyValue](https://github.com/apache/pulsar/pull/27375) | `stringToLong("")`/`stringToFloat("")` crashed with `NumberFormatException` while the Integer/Double siblings return `null` (their guard was never added to these two), and `setEmptyValue`'s String check compared the type object's class to `String.class` — always false — so blank values left stale Strings instead of clearing them — fixes [#27374](https://github.com/apache/pulsar/issues/27374), self-found by reading the config-parsing utilities against their own sibling patterns | 🟢 Open · two committer approvals (lhotari + codelipenghui) · first-contributor merge gate |

| Bug report | What it documents | Status |
|---|---|---|
| [#27377 — `RelativeTimeUtil` silently fabricates values for overflow-sized inputs](https://github.com/apache/pulsar/issues/27377) | every other malformed input raises, but `"15252526452552645w"` returns a wrapped garbage value — the JDK `TimeUnit` conversion saturates at `Long.MAX_VALUE` seconds and the week/year step then wraps it; measured on the project's own compiled classes | ⚪ Closed — fixed by community PR [#27464](https://github.com/apache/pulsar/pull/27464) (merged); our staged fix branch retired |

<a name="superset"></a>

## <img src="https://github.com/apache.png" width="24" alt="Apache"> Apache Superset (data visualization)

| Pull request | What it fixes | Status |
|---|---|---|
| [#46040 — reject deeply nested date expressions with a parse error](https://github.com/apache/superset/pull/46040) | `datetime_eval` converts only `ParseException`, but the date-expression grammar recurses once per nesting level — a pasted ~500-character time range (60–80 nested `dateadd(` calls, measured on master) exhausted the interpreter stack and hit the chart-data and Jinja paths as an unhandled `RecursionError` (500) instead of the parse error every other malformed expression produces — fixes [#46039](https://github.com/apache/superset/issues/46039), self-found by fix-commit mining the freshly-fixed date-parser area | ✅ Approved by aminghadersohi ("LGTM") · awaiting merge |
| [#46114 — support 'last day of' / 'last of' time range phrases](https://github.com/apache/superset/pull/46114) | the time-range lookup gave `first day of last quarter` a correct since-bound but silently degraded the until-bound to yesterday; the two new lookup entries mirror the first-day patterns with an end-of modifier — maintainer-verified ("the patterns resolve to the correct dates"), docs updated in-PR | ✅ Approved by aminghadersohi ("LGTM") · awaiting merge |

| Bug report | What it documents | Status |
|---|---|---|
| [#46162 — Python-Unit CI fails mcp_service tool tests on every pull request since Nov 10](https://github.com/apache/superset/issues/46162) | CI-health report with the full run-links evidence table and the master-green paradox; filed so reviewers know the red checks on PRs are upstream, not the PR | 🟡 Open — resolution evidence posted (environmental, outside the mcp_service path); offered closure |

<a name="argocd"></a>

## <img src="https://github.com/argoproj.png" width="24" alt="Argo"> Argo CD (CNCF)

| Pull request | What it fixes | Status |
|---|---|---|
| [#30892 — format float64 generator params as plain decimals for selector matching](https://github.com/argoproj/argo-cd/pull/30892) | `flattenParameters` formats generator parameter values with `fmt.Sprintf("%v", ...)`, and float64 renders via `%g` — JSON/YAML numbers ≥ 1e6 or < 1e-4 become scientific notation (`1.762e+09`), so a post-generator selector comparing `n=1762000000` silently never matches; now formatted in plain decimal notation — fixes [#30891](https://github.com/argoproj/argo-cd/issues/30891), self-found with a probe: `float64(1762000000)` → `"1.762e+09"`, selector match `false` | 🟢 Open · maintainer LGTM'd, review points addressed same-day (scope verified correct: only `goTemplate: true` paths) · awaiting formal approval |
| [#30924 — evaluate sync windows against the operation being processed](https://github.com/argoproj/argo-cd/pull/30924) | `setOperationState` patches the API server but never the in-memory app object, so `syncWindowPreventsSync` derived `isManual`/`operationStartTime` from the *previous* operation's stale status — after a manual sync, an always-on deny window with `manualSync: true` allowed the queued automated sync through. Unit-level repro: probe returned `blocked=false` with an active deny window — fixes [#30914](https://github.com/argoproj/argo-cd/issues/30914), root-caused from another user's report | 🟢 Open · CI green · awaiting review |
| [#30981 — clean error message for missing BitBucket branch hash](https://github.com/argoproj/argo-cd/pull/30981) | `BitBucketCloudProvider.GetBranches` checked-and-returned `err` at the top, then formatted `%w` with that guaranteed-nil error on a missing/non-string `target.hash` — users saw `error getting SHA for branch …: %!w(<nil>)` whenever BitBucket returned an odd payload; now a clean named message + regression test — fixes [#30980](https://github.com/argoproj/argo-cd/issues/30980), filed by us; same class as #30855, single site confirmed by package scan | 🟢 Open · CI green (lint round fixed same-session) · awaiting review |
| [#31036 — scope the diff cache by the diff strategy](https://github.com/argoproj/argo-cd/pull/31036) | cached app diffs were keyed without the diff strategy, so a result produced by one strategy could be reused by another — implements the maintainer-requested [#30969](https://github.com/argoproj/argo-cd/issues/30969): writes are strategy-scoped, a nil diffConfig skips the scoped write (a poisoned fallback can't be cached), and the unscoped key is dual-written so legacy server-side readers keep working; e2e caught the missing dual-write as a real `argocd app diff` regression before review — fixed same-session with a flow test pinning it | 🟢 Open · CI-complete — fully green 39/39 (lint + unit + all e2e shards) · CodeRabbit majors adopted, tests pin both strategy-flip transitions · awaiting review + the cache-settings design pick |

| Bug report | What it documents | Status |
|---|---|---|
| [#30891 — ApplicationSet: post-generator selector silently fails to match numeric params](https://github.com/argoproj/argo-cd/issues/30891) | scientific-notation rendering of float64 generator params breaks selector equality; scoping analysis posted with exact line refs (non-goTemplate paths stringify at the generator level = separate follow-up decision) | 🟡 Filed — fix open as #30892 |
| [#31042 — ApplicationSet: Azure DevOps SCM provider returns corrupted error (%!w(<nil>))](https://github.com/argoproj/argo-cd/issues/31042) | the #30981 sibling in the Azure DevOps provider — the same check-and-return-then-`%w` pattern renders a guaranteed-nil error into `%!w(<nil>)` on odd payloads; filed with the verified mechanism | 🟢 Open — **claimed by a community contributor**; analysis verified correct + gracious handover posted with a harness tip |

<a name="dapr"></a>

## <img src="https://github.com/dapr.png" width="24" alt="Dapr"> Dapr (CNCF)

| Bug report | What it documents | Status |
|---|---|---|
| [kit #179 — ISO 8601 duration parser accepts overflowing and negative components](https://github.com/dapr/kit/issues/179) | the parser accepts hours far beyond any sane range and negative durations — downstream the scheduler builds `@every` intervals from them, a `uint32` truncation fires, and negative repeat counts never decrement; filed with a probe table after checking the project's four open parser issues for overlap | 🟡 Filed — fix PR staged behind the in-flight parser PRs |
| [#11056 — actor reminder/timer APIs panic on a `null` body](https://github.com/dapr/dapr/issues/11056#issuecomment-6691551369) | confirmed the reporter's crash with a unit probe at both panic sites and pinned the mechanism: a `*struct` unmarshal target becomes nil on JSON `null`, then a field dereference panics | 🟢 Confirmed — repro + mechanism posted |
| [#11050 — an unknown CEL expression identifier hangs daprd in an infinite compile loop](https://github.com/dapr/dapr/issues/11050#issuecomment-6691611633) | confirmed with a probe that never returns: a compile error shares its message prefix with the "missing variable" path, so the expression recompiles forever — affects pubsub routing rules and circuit-breaker expressions | 🟢 Confirmed — repro + mechanism posted |
| [#11032 — outbox PublishInternal panics on multi-projection transactions](https://github.com/dapr/dapr/issues/11032#issuecomment-6745667701) | confirmed with an in-package probe running the issue's exact 4-operation batch: the strip loop mutates `operations` while ranging over it — each in-place shift reassigns the slice to a narrower view, so a later iteration dies with `slice bounds out of range [4:2]` and entries are skipped along the way | 🟢 Confirmed — repro + mechanism posted |

<a name="onnx"></a>

## <img src="https://github.com/onnx.png" width="24" alt="ONNX"> ONNX (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8758 — accept omitted optional inputs in Dropout](https://github.com/onnx/onnx/pull/8758) | the reference implementation picked `Dropout`'s optional inputs by position count, but the evaluator hands over an omitted optional input as `None` instead of dropping it — so a training-mode model that leaves out `ratio` (legal per spec; the default is 0.5) crashed with a `TypeError`, and every opset-12 node carrying the `training_mode` attribute failed before the implementation even ran. Found with a differential sweep that omits each optional input from all 1,876 node tests and runs the result through the reference evaluator — `Dropout` was the only op whose crash wasn't a deliberate validation guard | 🟢 Open · maintainer-approved (justinchuby) · CI awaiting first-time workflow approval |
| [#8760 — round QLinearConv before adding y_zero_point](https://github.com/onnx/onnx/pull/8760) | the reference quantized the accumulator with ties-to-even rounding *after* adding the zero point, while the spec rounds the quotient first — the orders disagree whenever the quotient is a half-integer and the zero point is odd (quotient 0.5 with zero point 1: spec 1, reference 2). Found by mining the merged QLinearMatMul fix (#8700) for unfixed siblings — `QLinearConv` was the one remaining op in the class | 🟢 Open · in review · CI awaiting first-time workflow approval |
| [#8772 — compute BatchNormalization training statistics in float32 for float16/bfloat16](https://github.com/onnx/onnx/pull/8772) | BatchNormalization's training-mode variance squares the input and overflows the float16 range above ~256 — output_var came out as `inf` with the true value still representable, and the output collapsed to zeros; now computed in float32 for float16/bfloat16 inputs — the same fix the maintainers shipped for InstanceNormalization, LRN, LogSoftmax and SoftmaxCrossEntropyLoss days earlier; found by sweeping the remaining normalization/reduction ops for the class. The running-statistics blend is also promoted (a float16-quantized previous mean corrupts through cancellation: -0.4 becomes 0 on the regression case). Rebased on current main — the LpNormalization sibling dropped (already subsumed by merged #8454, conflicting scope) and a float32-extremes case added | 🟢 Open · in review · all three Copilot findings addressed · `topic:`/`module:` label requested |
| [#8786 — compute LpPool in float32 for float16/bfloat16](https://github.com/onnx/onnx/pull/8786) | the pooling sibling of #8772: LpPool raised the input to the power `p` in the input dtype, so float16 windows containing values above 256 pooled to `inf` while the true L2 norms were representable. GlobalLpPool already computes in log space and needed nothing; found while sweeping the rest of the pool family | 🟢 Open · **maintainer-approved (justinchuby)** · docs regenerated generator-exact · `topic:`/`module:` label requested |

| Bug report | What it documents | Status |
|---|---|---|
| [#8811 — reference: CumSum and Sum produce wrong float16 results while the true value is representable](https://github.com/onnx/onnx/issues/8811) | the reduction siblings of the fixed normalization ops still accumulate in the input dtype — float16 CumSum/Sum lose precision or overflow where float32 accumulation would keep the exact result; filed with failing-first probes | 🟡 Filed — fix implemented and staged on the fork (opens per the project's PR etiquette) |

<a name="osquery"></a>

## <img src="https://github.com/osquery.png" width="24" alt="osquery"> osquery (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#9280 — reject truncated shellbag file-entry records instead of throwing](https://github.com/osquery/osquery/pull/9280) | `fileEntry()` subtracted 8 from the position of the `0400EFBE` signature it found anywhere in attacker-controlled shellbag data — a record starting with that signature underflowed the unsigned offset past its zero-check, and truncated records made `substr()` throw `std::out_of_range`, which the table layer turns into a failed query: one malformed registry value silently killed the entire `shellbags` query. Three guards now return the existing unsupported sentinel; found as the missed sibling of #9218's drive-item guards | ✅ **MERGED** by zwass |
| [#9283 — check netlink payload lengths before typed reads in routes](https://github.com/osquery/osquery/pull/9283) | the Linux routes table walked netlink attributes with `RTA_OK()`, which validates only the attribute *header* against the remaining bytes, then dereferenced the payloads unchecked — interface indexes, metrics and addresses were read as `int`/`inet_ntop` from buffers that could end mid-field. Every typed read now checks `RTA_PAYLOAD()`; ships with a byte-by-byte netlink test harness (the routes table's first) whose truncated-attribute cases read past the message on master | ✅ **MERGED** by mike-myers-aapl — he verified it with ASan+UBSan copies of the netlink macros (master fails, the PR passes) — the first osquery merge |
| [#9286 — reject truncated records in the remaining shellitem parsers](https://github.com/osquery/osquery/pull/9286) | eleven more shellbag parsers read fixed-offset fields with `substr()` and could throw on attacker-controlled truncated records, aborting the whole query — the file-entry fix (#9280) left these siblings behind. Every parser now rejects under-length records with its existing sentinel; nine tests craft records that end inside each parser's field reads | 🟢 **Approved by mike-myers-aapl** — he verified both round-4 fixes himself and resolved the Copilot threads · rebased onto master per zwass after the #9280 merge (40-test container re-run) · awaiting merge |
| [#9322 — guard the prometheus_targets config against malformed values](https://github.com/osquery/osquery/pull/9322) | the prometheus_metrics table read the `prometheus_targets` config section without validating its type — the config parser plugin copies the value verbatim and the table then called rapidjson `HasMember()`/`GetArray()`/`GetUint64()` on whatever shape it found, so a config value that is not an object fired rapidjson's `IsObject()` assertion (abort in debug builds, undefined behavior in release, since osquery does not override `RAPIDJSON_ASSERT`). The config value is user-controlled, so a typo broke the whole table. Every level is now validated with the file's `LOG(WARNING)` + graceful-return pattern, the logic moved into a testable `parsePrometheusTargetsConfig()` helper, and unit tests cover malformed and valid configurations — fixes [#9321](https://github.com/osquery/osquery/issues/9321) | ✅ **MERGED** by zwass — issue #9321 closed as completed; directionless's global-throwing-RAPIDJSON_ASSERT idea parked as a follow-up discussion |

<a name="zephyr"></a>

## <img src="https://github.com/zephyrproject-rtos.png" width="24" alt="Zephyr"> Zephyr RTOS (Linux Foundation)

| Pull request | What it fixes | Status |
|---|---|---|
| [#124926 — unlock interrupts on error paths in rx_enable](https://github.com/zephyrproject-rtos/zephyr/pull/124926) | `ifx_cat1_uart_async_rx_enable()` locked interrupts before validating its arguments and DMA state, but four error paths returned without unlocking — a caller passing a bad buffer or racing an active RX got the system frozen with interrupts disabled. Found by scanning every `irq_lock()` error path in `drivers/` after the same bug was fixed in two DMA drivers a day apart; maintainer requested a v4.5 backport — tracking issue [#124960](https://github.com/zephyrproject-rtos/zephyr/issues/124960) closed against the merged #124524 | ⚪ Closed — superseded by merged #124524 |
| [#124927 — unlock interrupts on invalid pin configurations](https://github.com/zephyrproject-rtos/zephyr/pull/124927) | two GPIO drivers returned `-ENOTSUP` from their configure callbacks with interrupts still locked — one rejected a pin set as both input and output, the other fell through the direction switch's default arm. Both now unlock before returning | ✅ **MERGED** (first Zephyr merge) |
| [#124961 — unlock interrupts on USB error paths](https://github.com/zephyrproject-rtos/zephyr/pull/124961) | the Renesas RA UDC returned `-EIO` from endpoint-dequeue with interrupts still locked when transfer abort failed, and the SAM USBC attach returned the pinctrl error the same way — leaving the system frozen after a rejected attach. Both now unlock before returning | ✅ **MERGED** by Anas Nashif (two maintainer approvals) |
| [#124962 — unlock interrupts on grant double-free](https://github.com/zephyrproject-rtos/zephyr/pull/124962) | Xen's grant-table release path logged a warning and returned from the double-free case with interrupts still locked — a repeated release froze the system permanently. Now unlocks before returning | ✅ **MERGED** by Anas Nashif (three maintainer approvals) |
| [#125508 — avoid 64-bit divisions in TDK temperature conversions](https://github.com/zephyrproject-rtos/zephyr/pull/125508) | two TDK sensor drivers divided 64-bit values by constants in their temperature math, pulling the software 64-bit division helper onto divider-less MCUs — the icm4268x decoder was the unfixed sibling of the already-reworked #124230 path. Rewritten in int32 with the reduced reciprocal, exhaustively equivalence-checked over the full input ranges | ✅ **MERGED** by Anas Nashif (two maintainer approvals) |
| [#125667 — close the connection on unexpected packet types](https://github.com/zephyrproject-rtos/zephyr/pull/125667) | the MQTT rx dispatcher treated packet types a client can never receive — CONNECT, SUBSCRIBE, UNSUBSCRIBE and PINGREQ (client-to-server only) plus reserved type 0 (MQTT v3.1.1 §2.2.1 / v5.0 §2.1.2) — as a no-op default case: the packet was silently dropped while the connection stayed open, leaving client and broker with diverging session state. Now validated right after the fixed header, before the claimed body is read, reporting `-EBADMSG` so the input loop disconnects with Protocol Error (0x82) through the existing errno mapping — fixes [#125514](https://github.com/zephyrproject-rtos/zephyr/issues/125514) | ✅ **MERGED** by Anas Nashif (jukkar + rlubos approvals) — Jukka's strengthened tests wired into the suite (body-never-arrives and oversized-RX-buffer cases discriminating the hoisted check); issue #125514 closed as completed |
| [#125797 — reset the MQTT disconnect reason between sessions](https://github.com/zephyrproject-rtos/zephyr/pull/125797) | the decoder sets `internal.disconnect_reason` on processing errors (topic alias invalid, implementation specific error) and `disconnect_5_0_notify()` prefers it over the errno mapping, but nothing ever clears it — after a reconnect on the same client instance the next error sent the previous session's reason. Now cleared in `client_reset()` (which runs after each DISCONNECT is sent), with a two-connection regression test: topic-alias violation gives 0x94 on the first DISCONNECT, the fresh session's own error gives 0x82 instead of leaking 0x94 — fixes [#125792](https://github.com/zephyrproject-rtos/zephyr/issues/125792) | ✅ **MERGED** by Anas Nashif (jukkar + rlubos approvals) — the issue closed as completed |
| [#125909 — clear MQTT topic alias mappings on connection reset](https://github.com/zephyrproject-rtos/zephyr/pull/125909) | the decoder learns broker topic aliases into the client instance and resolves alias-only PUBLISHes against that table, but nothing ever clears it — after a reconnect on the same client instance an alias-only PUBLISH silently resolved against the previous session's topics (MQTT 5.0 §3.3.4 limits alias mappings to one connection). Now cleared in `client_reset()` with a two-connection regression test: alias 1 taught on connection 1, then an alias-only PUBLISH must return `-EBADMSG` instead of resolving the stale topic — fixes [#125908](https://github.com/zephyrproject-rtos/zephyr/issues/125908) | ✅ **MERGED** by Anas Nashif (jukkar + rlubos + maass-hamburg approvals) — the issue closed as completed |
| [#126044 — avoid 64-bit divisions in sensor sample conversion](https://github.com/zephyrproject-rtos/zephyr/pull/126044) | the rm3100 magnetometer decoder divided a 64-bit value twice per sample (by the cycle-count divider, then by 100) and the icm20689 temperature conversion divided a 64-bit product by 3268 — both pulled the software 64-bit division helper onto divider-less cores on every conversion, the same class as the merged #125508. Both now run in int32 arithmetic (divisor powers of two folded into the shift, divisions composed and split into whole/remainder parts), with equivalence proven exhaustively over the full input ranges — fixes [#126043](https://github.com/zephyrproject-rtos/zephyr/issues/126043) | 🟢 Open · **approved by afontaine-invn** · awaiting maintainer merge |

<a name="botorch"></a>

## <img src="https://github.com/meta-pytorch.png" width="24" alt="BoTorch"> BoTorch (Meta)

| Pull request | What it fixes | Status |
|---|---|---|
| [#3550 — preserve float64 precision of a Python-float best_f](https://github.com/meta-pytorch/botorch/pull/3550) | the analytic acquisition functions document `best_f` as "either a scalar or a `b`-dim Tensor", but the scalar form was rounded through the default dtype at construction while the Tensor form kept full precision — and Expected Improvement is exponentially sensitive to `best_f`, so with a double model and a large-magnitude incumbent the two forms disagreed by 137 orders of magnitude (EI `7.07e-02` vs `1.51e-139`) — fixes [#3549](https://github.com/meta-pytorch/botorch/issues/3549), self-found by mining the just-merged `make_scipy_bounds` precision fix (#3542) for the same Python-scalar-through-default-dtype class across the acquisition package | 🟢 Open · all local tests green incl. new regression test · Meta CLA signature pending |
| [#3551 — preserve float64 precision of scalar best_f, tau and constraint bounds](https://github.com/meta-pytorch/botorch/pull/3551) | extends #3550 to the remaining sites of the same class: the qEI/qPI improvement buffers, qLogEI's buffer + `_log_improvement`, and the constrained-acquisition mixin's `con_lower/con_upper/con_both` value buffers (cast to `torch.double` + `.to(means)` casts in the feasibility funnel) — infeasible_cost and risk-measure buffers pattern-flagged but deliberately out of scope (not repro-verified) | 🟢 Open · Meta CLA green at open · awaiting review |

<a name="pytorch"></a>

## <img src="https://github.com/pytorch.png" width="24" alt="PyTorch"> PyTorch (Meta)

| Pull request | What it fixes | Status |
|---|---|---|
| [#203846 — make inductor's index_reduce validation match eager](https://github.com/pytorch/pytorch/pull/203846) | Inductor's own decomposition of `aten.index_reduce` checked devices but skipped the shape/dtype checks eager applies, so a scalar `self` with a 1-dim `source` broadcast through the mean path and silently returned `3.5` where eager raises "source tensor shape must match self tensor shape" — fixes [#202938](https://github.com/pytorch/pytorch/issues/202938), reproduced locally through the full raw/eager/aot_eager/inductor matrix after setting up MSVC + Windows SDK for torch.compile on this machine | 🟢 Open · `in progress` — two automated-review rounds processed (blocking rank/SymBool shape-check flaw fixed via the index_copy pattern, source-dim bounds check restored, scatter path collapsed) |
| [#204077 — remove unsound Partial(max/min) preservation for nan_to_num partial reductions](https://github.com/pytorch/pytorch/pull/204077) | the DTensor op registration preserved a `Partial(max)`/`Partial(min)` shard prop through `nan_to_num`'s amplitude-clamping rewrites, so partial reductions silently returned wrong values (amax 5 vs 0, posinf 5 vs -1 on a Shard(0) tensor) — the three overloads deleted so DTensor materializes to Replicate first, regression test added to the distributed suite; completed the reporter's missing verification (their environment predated the bug) by running the issue's end-to-end repro fail-first on the 2.13 wheel — fixes [#203922](https://github.com/pytorch/pytorch/issues/203922); automated review processed same-session (5 findings implemented, 1 refuted with an empirical repro that disproved its claim) | 🟢 Open · **APPROVED by @aditvenk (DTensor team)** — `ready for review`, at the merge gate awaiting a committer |
| [#203849 — inductor's index_add has the same missing shape validation](https://github.com/pytorch/pytorch/issues/203849) | the sibling decomposition in the same file skips eager's shape check too: a scalar `self` with a 1-dim `source` silently returns `7.0` where eager raises — found by probing the next op in the family while the index_reduce fix was in CI | 🟡 Issue filed · awaiting `actionable` label · PR queued behind it |

| Bug report | What it documents | Status |
|---|---|---|
| [#203631 — SGD silently accepts out-of-range dampening values](https://github.com/pytorch/pytorch/issues/203631) | SGD checks `lr`, `momentum` and `weight_decay` but not `dampening`, so values outside [0, 1] are silently accepted and the momentum buffer extrapolates instead of interpolating — on both the foreach and single-tensor paths; every sibling optimizer already validates its range-bounded parameters — self-found by comparing each optimizer's validators against the parameters its update math actually consumes; community-sharpened: sanchit1707's fixed-point analysis (buf* = 10·(1−d) — silent 15× amplification or sign reversal, not unbounded growth) verified numerically and endorsed | 🟡 Issue filed · reproduced + PR-offered by the community · awaiting maintainer range-confirmation |
| [#204084 — sign/sign_ preserve Partial(max/min) but sign(NaN) = 0 breaks the invariant](https://github.com/pytorch/pytorch/issues/204084) | follow-up from the #204077 verification: `sign(NaN)=0` while `max(sign(0), sign(5))=1`, so the preserved shard prop is unsound for sign too — verified empirically before filing; hardshrink/threshold/relu/round keep NaN so unaffected | ✅ **Closed as completed** — fixed by [#205431](https://github.com/pytorch/pytorch/pull/205431) removing the whole class of NaN-unsound partial pass-through rules; our repro now quoted in the code comment, fix verified against main's table |
| [#204083 — in-place nan_to_num_ on a Partial(max/min) DTensor still silently unsound](https://github.com/pytorch/pytorch/issues/204083) | follow-up from the #204077 automated review: the in-place path runs silently with the shard prop preserved, giving [5.0, 2.0] vs correct [0.0, 2.0] — a pre-existing defect unchanged by our PR, filed instead of writing the false BC note | ⚪ Closed as covered by #204077 (the silent path only exists on ≤2.13 wheels; removed going forward) |

<a name="actual"></a>

## <img src="https://github.com/actualbudget.png" width="24" alt="Actual Budget"> Actual Budget

| Pull request | What it fixes | Status |
|---|---|---|
| [#9416 — reject amounts too large for safe arithmetic on import](https://github.com/actualbudget/actual/pull/9416) | importing a CSV whose amount overflows the safe-integer range crashed the transaction list on render; the import preview now rejects such rows like other unparseable fields — fixes [#9415](https://github.com/actualbudget/actual/issues/9415) | 🟢 Open · all CI green · every review thread resolved · in review |
| [#9419 — return focus to the input after picking a calendar day](https://github.com/actualbudget/actual/pull/9419) | picking a date in the calendar dropped keyboard focus, forcing mouse-only transaction entry — fixes [#9370](https://github.com/actualbudget/actual/issues/9370) | 🟢 Open · in review |

<a name="agno"></a>

## <img src="https://github.com/agno-agi.png" width="24" alt="agno"> agno

| Bug report | What it documents | Status |
|---|---|---|
| [#11414 — `LinearTools.update_issue` rejects its own documented call](https://github.com/agno-agi/agno/issues/11414) | GraphQL `$title: String!` non-null variable bound to `None` — the documented "title unchanged" call always fails; state updates advertised but impossible | 🟡 Reported · community contributor implementing; our fix + 6 tests staged |
| [#11415 — `custom_scrape_website` returns field names instead of scraped data](https://github.com/agno-agi/agno/issues/11415) | dict-key iteration returned the query's schema instead of the page content; also repaired the module's broken test fixtures and revived a maintainer-skipped test | 🟡 Reported · community contributor implementing; our fix + tests staged |
| [#11421 — toolkit HTTP calls without a timeout can hang the agent thread](https://github.com/agno-agi/agno/issues/11421) | `requests` call sites in 2 toolkits wait forever on a degraded upstream — scope corrected after a community fact-check confirmed Bright Data/Serply were already fixed | 🟡 Reported · handed to a community contributor with the corrected scope |

<a name="aws-amplify"></a>

## <img src="https://github.com/aws-amplify.png" width="24" alt="AWS Amplify"> AWS Amplify (JavaScript)

| Pull request | What it fixes | Status |
|---|---|---|
| [#15022 — encode UTF-8 bytes in the OAuth customState helpers](https://github.com/aws-amplify/amplify-js/pull/15022) | `urlSafeEncode` emitted a variable number of hex digits per code unit while `urlSafeDecode` always read 2 — any `signInWithRedirect` custom state above `U+00FF` (Polish, Greek, Arabic, CJK, emoji) came back corrupted and broke `JSON.parse` of the `customOAuthState` Hub event; v5-stable side of [#15019](https://github.com/aws-amplify/amplify-js/issues/15019) | 🟢 Open · on v5-stable · 14 tests, ASCII byte-for-byte identical |

<a name="crewai"></a>

## <img src="https://github.com/crewAIInc.png" width="24" alt="crewAI"> crewAI

| Pull request | What it fixes | Status |
|---|---|---|
| [#8845 — store sqlite checkpoint data as plain text](https://github.com/crewAIInc/crewAI/pull/8845) | checkpoint writes crash on SQLite < 3.45 (`no such function: jsonb`) — fixes [#8843](https://github.com/crewAIInc/crewAI/issues/8843) | 🟢 Open · CI green · in review |
| [#8848 — publish JSON checkpoints atomically](https://github.com/crewAIInc/crewAI/pull/8848) | interrupted writes left truncated/corrupt checkpoint files — fixes [#8846](https://github.com/crewAIInc/crewAI/issues/8846) | 🟢 Open · CI green · in review |
| [#8849 — tolerate malformed tool-call arguments in history replay](https://github.com/crewAIInc/crewAI/pull/8849) | uncaught `JSONDecodeError` crash replaying Anthropic/Bedrock conversations — fixes [#8847](https://github.com/crewAIInc/crewAI/issues/8847) | 🟢 Open · CI green · in review |

<a name="weathergen"></a>

## <img src="https://github.com/ecmwf.png" width="24" alt="ECMWF"> ECMWF WeatherGenerator

| Pull request | What it fixes | Status |
|---|---|---|
| [#3028 — TrainLogger takes run_id and results path instead of the global config](https://github.com/ecmwf/WeatherGenerator/pull/3028) | the training logger held the entire global config object but only ever read the run id from it — now it takes the two parameters it needs and can be used standalone — fixes the remaining scope of [#1213](https://github.com/ecmwf/WeatherGenerator/issues/1213) | ⚪ Closed unmerged — the maintainer swept external PRs; the repo no longer accepts outside pull requests |
| [#3030 — fix legacy metrics lookup level](https://github.com/ecmwf/WeatherGenerator/pull/3030) | the metrics-file backwards-compatibility branch probed a path no released version ever wrote, so reading any pre-rename run crashed with `FileNotFoundError` instead of using the compat file — fixes [#3029](https://github.com/ecmwf/WeatherGenerator/issues/3029), a self-found bug traced through the #601/#1831 history | ⚪ Closed unmerged — same external-PR sweep |
| [#3032 — fix bare-path config entries in compare_run_configs](https://github.com/ecmwf/WeatherGenerator/pull/3032) | the config-comparison tool's bare-path format crashed with a doubled directory path ever since a config-loader fix changed `model_path` semantics — fixes [#3031](https://github.com/ecmwf/WeatherGenerator/issues/3031), self-found and reproduced end-to-end before filing | ⚪ Closed unmerged — same external-PR sweep |

<a name="fastmcp"></a>

## <img src="https://github.com/PrefectHQ.png" width="24" alt="fastmcp"> fastmcp

| Pull request | What it fixes | Status |
|---|---|---|
| [#6180 — decode RFC 6901 escapes when extracting `$defs` names](https://github.com/PrefectHQ/fastmcp/pull/6180) | JSON-pointer-escaped schema names broke schema extraction — fixes [#6034](https://github.com/PrefectHQ/fastmcp/issues/6034) | ✅ Merged — maintainer finalized the branch himself before merging |
| [#6185 — keep `tools/list` working when a root `$ref` resolves to a boolean schema](https://github.com/PrefectHQ/fastmcp/pull/6185) | whole-server tools listing crashed on valid schemas — fixes [#6125](https://github.com/PrefectHQ/fastmcp/issues/6125) | ✅ Merged |
| [#6187 — support non-identifier variables in URI templates](https://github.com/PrefectHQ/fastmcp/pull/6187) | `{$top}`-style template variables never matched or forwarded; Unicode word characters that identifiers reject also disabled templates | ✅ Merged |
| [#6214 — apply tool transforms before tag filters on single servers](https://github.com/PrefectHQ/fastmcp/pull/6214) | tags added by a server's `tools` config were invisible to `include_tags`/`exclude_tags` on single-server MCPConfigs — fixes [#6196](https://github.com/PrefectHQ/fastmcp/issues/6196) | ✅ Merged |
| [#6188 — keep result hydration faithful for union coercions](https://github.com/PrefectHQ/fastmcp/pull/6188) | `0 → False`-style coercions silently replaced typed results; final guard also preserves schema-intended `format: json` decodes and rejects precision-losing timestamp truncation | 🟡 Open · survived three adversarial review rounds with same-session fixes · refreshed onto current main (42+10 tests green on the rebased head) · gate failing pending [#6136](https://github.com/PrefectHQ/fastmcp/issues/6136) assignment — the bot now keeps the PR open |
| [#6440 — compare pinned tool versions PEP 440-normalized against the listed version](https://github.com/PrefectHQ/fastmcp/pull/6440) | calling a versioned tool by an equivalent version spelling (`"1"` for a listed `"1.0"`) ran the listed tool but silently skipped output-schema hydration and result revalidation, because the client compared versions as strings while the server matches PEP 440-normalized — fixes [#6439](https://github.com/PrefectHQ/fastmcp/issues/6439) | 🔒 Bot-closed under the require-issue-link gate — auto-reopens if [#6439](https://github.com/PrefectHQ/fastmcp/issues/6439) is assigned |
| [#6585 — skip yanked releases in the PyPI version check](https://github.com/PrefectHQ/fastmcp/pull/6585) | `_fetch_latest_version` takes max() over PyPI's `releases` map including yanked releases — pip/uv refuse to resolve a fully-yanked release, so one yank makes the CLI upgrade notice recommend an uninstallable version indefinitely (sharpest in prerelease mode where RC yanks are routine; latent today — verified live: 149 releases, none yanked). Releases whose every file is yanked are skipped; empty file lists and partial yanks kept (safe direction) — fail-first: 2 tests red on main, 30/30 green on the branch — fixes [#6584](https://github.com/PrefectHQ/fastmcp/issues/6584), filed by us | 🔒 Bot-closed under the require-issue-link gate — auto-reopens if [#6584](https://github.com/PrefectHQ/fastmcp/issues/6584) is assigned |

| Bug report | What it documents | Status |
|---|---|---|
| [#6584 — the PyPI version check can recommend a yanked (unresolvable) release](https://github.com/PrefectHQ/fastmcp/issues/6584) | the max() over PyPI's releases map ignores yank status, which pip's resolver drops during resolution — the mismatch makes an uninstallable version look installable to the upgrade nag; filed with the live verification (149 releases, none yanked today) | 🟡 Filed — awaiting triage; fix open as [#6585](https://github.com/PrefectHQ/fastmcp/pull/6585) (bot-gated until assignment) |

<a name="layer5"></a>

## <img src="https://github.com/layer5io.png" width="24" alt="layer5"> layer5

| Pull request | What it fixes | Status |
|---|---|---|
| [#8277 — case-study banner fits its container on mobile](https://github.com/layer5io/layer5/pull/8277) | logo/graphic overflowed on small viewports — fixes [#8272](https://github.com/layer5io/layer5/issues/8272) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8278 — pricing cards reference real tier names](https://github.com/layer5io/layer5/pull/8278) | bylines named tiers that don't exist ("Free", "Team") — fixes [#8258](https://github.com/layer5io/layer5/issues/8258) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8279 — Sistent icons docs: valid imports, preview matches snippet](https://github.com/layer5io/layer5/pull/8279) | docs snippet imported non-existent exports; preview didn't match the code — fixes [#8257](https://github.com/layer5io/layer5/issues/8257) | ⚪ Reviewed "no changes needed" · closed in favor of the maintainer-assigned [#8291](https://github.com/layer5io/layer5/pull/8291), which merged |
| [#8280 — Heading 1 design token stays in viewport on mobile](https://github.com/layer5io/layer5/pull/8280) | 6rem default heading overflowed phones — fixes [#8267](https://github.com/layer5io/layer5/issues/8267) | 🟢 Reviewed "no changes needed" · awaiting merge |
| [#8281 — carousel arrows visible and clickable on mobile](https://github.com/layer5io/layer5/pull/8281) | arrows flickered, clipped off-screen at ≤ 850px — fixes [#8275](https://github.com/layer5io/layer5/issues/8275) | 🟢 Reviewed "no changes needed" · awaiting merge |

<a name="mem0"></a>

## <img src="https://github.com/mem0ai.png" width="24" alt="mem0"> mem0

| Pull request | What it fixes | Status |
|---|---|---|
| [#7795 — close owned pgvector connection pools on `Memory.close()`](https://github.com/mem0ai/mem0/pull/7795) | long-running hosts ran out of Postgres connections; now self-contained: `PGVector.close()` + ownership tracking + the `Memory.close()` wiring + a live-server regression test — fixes [#7771](https://github.com/mem0ai/mem0/issues/7771). Verified in production by the issue reporter | 🔒 Bot-closed under the issue-triage gate — auto-reopens if [#7771](https://github.com/mem0ai/mem0/issues/7771) is accepted |
| [#7797 — apply every operator on multi-operator Qdrant filters (TS SDK)](https://github.com/mem0ai/mem0/pull/7797) | `ne`/`nin` merged into one clause; `AND` branches overwrote each other — fixes [#7762](https://github.com/mem0ai/mem0/issues/7762) | 🔒 Bot-closed under the issue-triage gate — auto-reopens if [#7762](https://github.com/mem0ai/mem0/issues/7762) is accepted |
| [#7808 — honor explicitly configured default user_id in the Hermes plugin](https://github.com/mem0ai/mem0/pull/7808) | placeholder-collapse made an explicitly chosen default pool unreachable; gateway-native ids stranded memories — fixes [#7799](https://github.com/mem0ai/mem0/issues/7799) | 🔒 Bot-closed under the issue-triage gate — auto-reopens if [#7799](https://github.com/mem0ai/mem0/issues/7799) is accepted |

<a name="nicegui"></a>

## <img src="https://github.com/zauberzeug.png" width="24" alt="NiceGUI"> NiceGUI

| Pull request | What it fixes | Status |
|---|---|---|
| [#6468 — fix missing Torus export from the scene objects package](https://github.com/zauberzeug/nicegui/pull/6468) | `Torus` shipped in 3.19.0 with a scene method but the objects package forgot the import and `__all__` entry, so the documented import path raised `ImportError` | ⚪ Closed — same fix already open as [#6461](https://github.com/zauberzeug/nicegui/pull/6461) by the issue reporter and scheduled for 4.1 |

<a name="ollama"></a>

## <img src="https://github.com/ollama.png" width="24" alt="ollama-python"> ollama-python

| Pull request | What it fixes | Status |
|---|---|---|
| [#784 — skip blank lines in streaming NDJSON responses](https://github.com/ollama/ollama-python/pull/784) | a blank line anywhere in a streamed body (proxies, compatible servers re-chunking responses) crashed `generate(stream=True)` / `chat(stream=True)` with a raw `JSONDecodeError` | 🟡 Open · awaiting review |
| [#785 — union tool parameter types serialize as a JSON Schema type array](https://github.com/ollama/ollama-python/pull/785) | union parameter types produced an invalid comma-joined `type` (`"string, integer"`), nondeterministically ordered | 🟡 Open · awaiting review |
| [#786 — `Message.get` aligned with `__contains__` semantics](https://github.com/ollama/ollama-python/pull/786) | declared-but-unset fields returned `None` instead of the caller's default, and non-field names leaked through `.get()` | 🟡 Open · awaiting review |
| [#788 — `ResponseError` survives non-object JSON error bodies](https://github.com/ollama/ollama-python/pull/788) | a gateway/proxy error body of `null`, `[]`, or a bare JSON string crashed error construction with `AttributeError`, masking the real HTTP failure | 🟡 Open · awaiting review |

| Bug report | What it documents | Status |
|---|---|---|
| [#787 — `Tool.model_dump()` leaks the `defs` field name instead of `$defs`](https://github.com/ollama/ollama-python/issues/787) | verified serialization asymmetry between direct dumps and request-path dumps; two fix options documented for maintainers | 🟡 Awaiting maintainer decision — PR offered |

<a name="pypdf"></a>

## <img src="https://github.com/py-pdf.png" width="24" alt="pypdf"> pypdf

| Pull request | What it fixes | Status |
|---|---|---|
| [#4353 — guard the remaining non-dictionary /Resources accesses](https://github.com/py-pdf/pypdf/pull/4353) | two code paths (font listing and inline-image color-space lookup) still crashed with `TypeError` when `/Resources` was not a dictionary — the same robustness class fixed twice elsewhere in the codebase — fixes [#4352](https://github.com/py-pdf/pypdf/issues/4352), a self-found bug located by mining that repeated fix pattern | ✅ Merged — after the full review cycle: coverage requested and covered, five maintainer suggestions applied (two test-proven corrections to the suggestions themselves) |
| [#4420 — raise PdfReadError for a non-array trailer /ID](https://github.com/py-pdf/pypdf/pull/4420) | a corrupted trailer whose `/ID` entry is a non-array value (e.g. a bare string) is silently exposed inside the document instead of raising a read error — now a clean `PdfReadError` with probe tables — fixes [#4418](https://github.com/py-pdf/pypdf/issues/4418), filed by us | 🟢 Open · three review rounds addressed (round 3: stefan's exact-message match applied as an anchored regex) · stefan keeps the branch current with his own merge commits (strong pre-merge signal) · awaiting final re-review |
| [#4475 — resolve indirect /Info entries in the metadata properties](https://github.com/py-pdf/pypdf/pull/4475) | `DictionaryObject.get()` returns indirect `/Info` entries unresolved, so every metadata property except `title` returned None for values the document carries (author/subject/creator/producer/keywords/both dates) and the `*_raw` properties leaked `IndirectObject` — the read-side remainder of historical #1183, proven with a hand-built computed-xref PDF on main 7.1.1; entries are resolved in `metadata`'s copy loop (one spot, all 14 properties) — 14 parametrized cases red on main, green on the branch. Martin Thoma (lead) reviewed within ~5h; his crash-regression catch (undefined refs: `get_object` returns None, never raises) fixed same-session along with his two parametrized tests adopted verbatim | 🟢 Open · lead-reviewed, all findings handled · awaiting maintainer decision on [#4474](https://github.com/py-pdf/pypdf/issues/4474)'s keep/close |

| Bug report | What it documents | Status |
|---|---|---|
| [#4474 — indirect /Info entries make every metadata property but `title` return None](https://github.com/py-pdf/pypdf/issues/4474) | the spec allows indirect text strings in `/Info`; filed with the computed-xref probe and the full property matrix | 🟡 Open — stefan asked for a real-world sample: 181 real-world PDFs scanned, zero indirect /Info entries (honest result posted); keep/close handed to maintainers |
| [#4462 — FloatObject NaN/Infinity crash at serialization time](https://github.com/py-pdf/pypdf/issues/4462#issuecomment-6995769649) | `repr(NaN)` raises ValueError and `repr(inf)` OverflowError at `myrepr()` (`int(log10(abs(self)))` with no isfinite guard) — confirmed on 6.14.2 with the stronger round-trip evidence: one non-finite number makes a readable document unserializable via `write_to_stream`; the raw-token framing was corrected after stefan's challenge (the vector is programmatic — numpy pipelines produce inf without raising) | 🟢 Confirmed — verified repro posted; small isfinite-guard PR offered, fires on maintainer acceptance |

<a name="powertools"></a>

## <img src="https://github.com/aws-powertools.png" width="24" alt="Powertools"> Powertools for AWS Lambda (Python)

| Pull request | What it fixes | Status |
|---|---|---|
| [#8757 — ignore malformed `POWERTOOLS_PARAMETERS_MAX_AGE` instead of crashing](https://github.com/aws-powertools/powertools-lambda-python/pull/8757) | an empty or non-integer cache-TTL environment variable raised a raw `ValueError` from all 12 Parameters/Secrets/AppConfig entry points before any AWS call; now warns and falls back to the documented default per the project's compatibility ADR — fixes [#8747](https://github.com/aws-powertools/powertools-lambda-python/issues/8747) | ✅ Merged — maintainer ran the whole parameters suite on develop before approving; released in v3.41.0, credited by name in the release notes |

<a name="rai-toolkit"></a>

## <img src="https://github.com/wandb.png" width="24" alt="rai-toolkit"> rai-toolkit (Weights & Biases)

| Pull request | What it fixes | Status |
|---|---|---|
| [#130 — report model-ref load failures without a traceback](https://github.com/wandb/rai-toolkit/pull/130) | `rai assess <model-ref>` crashed with raw Python tracebacks for malformed refs, missing modules, and missing classes — now a clean input error, while a valid model's own factory or constructor failures keep their original exception and traceback | ✅ Merged — after a full human review cycle: changes requested on the exception boundary, corrected to the maintainer's spec, approved |

<a name="reflex"></a>

## <img src="https://github.com/reflex-dev.png" width="24" alt="reflex"> reflex

| Pull request | What it fixes | Status |
|---|---|---|
| [#7701 — keep literal `reflex.Var` tag text from hanging or corrupting string vars](https://github.com/reflex-dev/reflex/pull/7701) | any string prop containing literal `<reflex.Var>…</reflex.Var>` text hung the compiler in an infinite loop, crashed with `KeyError`/`IndexError`, or silently lost the text in rendered output | ⚪ Closed by the maintainer — approach declined (no use case for the syntax); accepted gracefully |
| [#7703 — `rx.asset(shared=True)` crash on Windows without Developer Mode](https://github.com/reflex-dev/reflex/pull/7703) | symlink creation denied → whole app failed to compile; fix falls back to hardlink, then to a writable copy, keeping later compiles replaceable | 🟡 Open · passed three rounds of automated review · awaiting human review |
| [#7704 — remove unused `path_ops.ln`](https://github.com/reflex-dev/reflex/pull/7704) | the public path helper did the exact opposite of `ln -s` semantics; the maintainer, on review, preferred removing it once the zero-callers search was confirmed — the PR was converted to the removal with a breaking-change changelog note | 🟡 Open · converted to removal on the maintainer's review · awaiting merge |
| [#7707 — drop the f-string Var marker from array ref names](https://github.com/reflex-dev/reflex/pull/7707) | the array ref formatter folded a per-run hash into compiled ref names, defeating reproducible builds — follow-up to #7691 | ✅ Merged by the maintainer |

| Bug report | What it documents | Status |
|---|---|---|
| [#7705 — hardlink/copy fallback assets aren't cleaned up when sources vanish](https://github.com/reflex-dev/reflex/issues/7705) | design question with three solution options; tracked in the project's internal backlog (ENG-13670) | 🟡 Awaiting maintainer decision |

<a name="simple-invoicing"></a>

## <img src="https://github.com/nikhilb2.png" width="24" alt="simple_invoicing"> simple_invoicing

| Pull request | What it fixes | Status |
|---|---|---|
| [#677 — reject whitespace-only API key names](https://github.com/nikhilb2/simple_invoicing/pull/677) | `POST /api/api-keys/` saved a name of only spaces as an empty string; now returns 422 | ✅ Merged — within the hour of opening |
| [#678 — reject blank units and unknown statuses on product update](https://github.com/nikhilb2/simple_invoicing/pull/678) | product updates silently accepted a blank unit and any status string; now reuses the create-path unit validation and bounds status to active/inactive with 422s | ✅ Merged — the same day, after addressing a maintainer change request with the requested API-level test |

---

*This page is the running index — every status above is live-verified against the GitHub API before each update. Reviews, merges and closures move the numbers in the header.*

**Open to internships and entry-level backend / infrastructure roles** · [GitHub](https://github.com/AP24110011695) · [LinkedIn](https://www.linkedin.com/in/ayush-kumar-saha-5126b6379)