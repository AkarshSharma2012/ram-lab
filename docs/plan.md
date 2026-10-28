# Ram Lab: research and implementation plan

Planning snapshot: October 27, 2026, America/Los_Angeles. Application implementation is not authorized yet. Repository creation, public visibility, workflow setup, planning artifacts, and GitHub Pages documentation are authorized. Every discrete change must receive a separate commit, including individual background-color or font changes. Public repository: https://github.com/AkarshSharma2012/ram-lab.

## Recommendation

Build Ram Lab as a local experiment supervisor and forensic reporting extension around existing effect-testing infrastructure. Start with a file-format adapter for Agent Crash Test, rather than recreate its mutation catalog or report UI. Add an original experiment layer for real agent workloads, verified worker-process death/restart, claim-versus-effect analysis, and Excel exports that retain evidence identity. Keep upstream optional and pinned. A two-day, post-approval compatibility spike decides whether to integrate its JSON results, make a small attributed fork, or use an independent minimal effect fixture.

The differentiation hypothesis is the **joint experiment**: when an actual agent builds an app, answers a source-grounded assignment, or solves math under a controlled fault schedule, can we show what physically happened, what the agent claimed, whether the claim was supported, and whether recovery preserved the intended result? Fault injection, side-effect contracts, checkpoints, factuality scoring, trace viewers, and Excel export are individually established ideas. No claim is made that no equivalent system exists.

Strongest counterargument: Agent Crash Test already covers lost responses after commits, physical calls, effect contracts, evidence, timelines, and a local HTML interface. DeepAgentLabs combines chaos, evaluations and observability across its ecosystem. Ram Lab could become a report-format wrapper with little engineering contribution. The answer must be a demonstrated new, reproducible experiment with an independently verified crash boundary and claim/effect discrepancy, not a longer feature list.

## 1. Research coverage and evidence limits

Primary repositories and documentation were read on October 27. README capabilities below are publisher claims, not locally verified runtime behavior. License files were inspected for the four initial open-source leads, Agent Crash Test, and Langfuse. No competitor packages were installed or benchmarked. No market demand or internship preference has been established. Review sample: zero systematically collected user reviews; no complaint percentages or fabricated quotations are used. This is an engineering opportunity assessment, not a validated business case.

Evidence labels: **D** = documented in inspected primary sources; **P** = partly documented or different semantics; **U** = not established by the inspected sources. U does not mean absent. All runtime capability claims remain untested locally. Current branch heads are recorded separately in source-register.json; a branch head read after a file is not proof that the file was fetched at that commit. Pin and re-read the selected dependency during the compatibility spike.

| Project | Injection and experiments | Recovery and physical effects | Claims and evaluation | Reports and cost | Reuse boundary and implication |
|---|---|---|---|---|---|
| floritange/AgentChaos | D: HTTP-response perturbation; content/tool-call corruption, timeouts and batch evaluation | P: its fault taxonomy includes API failures called crash faults; actual worker termination and durable effect reconciliation are U | P: fault diagnosis; claim-by-claim supporting/contradicting evidence is U | D: raw versus delivered response, tokens, timing and JSON trace | MIT file inspected. Useful optional HTTP fault adapter; the README's crash category must not be described as verified OS-process death. [S01](https://github.com/floritange/AgentChaos/blob/main/README.md), [license](https://github.com/floritange/AgentChaos/blob/main/LICENSE) |
| Nuuvixx/agentchaos | D: seeded infrastructure faults, baseline/fault/mitigation runners | D: semantic checkpoint cache with disk persistence; P: cache reuse is not proof of post-commit crash recovery | P: task success and cascade metrics; claim-level evidence is U | D: per-call latency, tokens and estimated costs | MIT file inspected. Direct overlap with a generic checkpoints-versus-retries project. README itself limits some wider research claims. [S02](https://github.com/Nuuvixx/agentchaos/blob/main/README.md), [API](https://github.com/Nuuvixx/agentchaos/blob/main/docs/api.md), [license](https://github.com/Nuuvixx/agentchaos/blob/main/LICENSE) |
| DeepAgentLabs/agentic-chaos | D: provider/tool/handoff/stream faults, scoped declarative campaigns, contracts and topology fuzzing | D: recovery contracts and bounded retries; P: workflow resume at a human gate differs from restart after OS death | D: fidelity judge adapters; U: a normative per-claim evidence table spanning process death | D: JSON reports, call logs, usage/cost recording and integrations | MIT file inspected. Strong option for broad fault coverage. Its AIOS export deliberately does not infer retry chains or promote detected faults to recovered states. [S03](https://github.com/DeepAgentLabs/agentic-chaos/blob/main/README.md), [contracts](https://github.com/DeepAgentLabs/agentic-chaos/blob/main/docs/v0.6.md), [workflow semantics](https://github.com/DeepAgentLabs/agentic-chaos/blob/main/docs/v0.8.md), [license](https://github.com/DeepAgentLabs/agentic-chaos/blob/main/LICENSE) |
| llmmas-otel | D: configurable A2A, tool and LLM fault injection with seeded selection | P: aligned fault traces; persistent effect oracle and actual process restart are U | P: fault ground truth/message capture; claim-level factuality is U | D: OpenTelemetry spans, message hashes, optional full message store | Apache-2.0 file inspected. Good interoperability reference; do not confuse the code license with the paper's redistribution terms. [S04](https://github.com/vagabondboffin/llmmas-otel/blob/main/README.md), [S07 paper, August 25, 2026](https://arxiv.org/html/2608.24271v1), [license](https://github.com/vagabondboffin/llmmas-otel/blob/main/LICENSE) |
| Langfuse | D: observations, evaluation datasets and experiments; a chaos controller is U | P: can hold evidence and scores; does not establish Ram Lab's effect-reconciliation contract | D: manual/code/model evaluations and comparison workflows | D: token/cost capture, inferred prices and observability UI | License is mixed: identified enterprise directories have separate terms; other applicable code is MIT. Prefer API/OTel integration, not copying its UI. [S05 costs](https://langfuse.com/docs/observability/features/token-and-cost-tracking), [S06 evaluations](https://langfuse.com/docs/evaluation/overview), [license](https://github.com/langfuse/langfuse/blob/main/LICENSE) |
| Agent Crash Test | D: bounded mutations, MCP proxy and JSONL bridge; ambiguous commits and duplicate delivery | D: physical calls, explicit effect contracts, observer evidence, inconclusive missing state | P: compares final promises to real effects; general claim extraction/evidence scoring is U | D: JSON/HTML/Markdown and CI outputs; local timeline UI; XLSX is U | MIT file inspected. Closest match and preferred integration candidate. README is a source preview; older project docs mark some now-advertised capabilities P1. Resolve documentation drift in the spike. [S08](https://github.com/pavloparaschakis/agent-crash-test/blob/main/README.md), [S09 test model](https://github.com/pavloparaschakis/agent-crash-test/blob/main/docs/project/06-test-model.md), [S10 reporting](https://github.com/pavloparaschakis/agent-crash-test/blob/main/docs/project/10-reporting-and-github-integration.md), [license](https://github.com/pavloparaschakis/agent-crash-test/blob/main/LICENSE) |
| RefChecker | Not a chaos harness | Not a recovery system | D: claim extraction, checking, aggregation and reference localization | D: fine-grained checking pipeline and demo | Methodological overlap. No code/data reuse selected; license and dataset terms must be checked before any import. [S11](https://github.com/amazon-science/RefChecker/blob/main/README.md) |
| AgentHallu | Benchmark of agent hallucination attribution, not this proposed crash experiment | Fault-to-claim attribution is an existing research problem | D: trajectory-level labels and responsible-step attribution | D: human-curated evaluation methodology | Do not claim inventing agent hallucination localization. Its published results are not Ram Lab measurements. No dataset reuse selected. [S13 paper, January 11, 2026](https://arxiv.org/html/2601.06818v1) |
| LangGraph persistence | Runtime support, not a complete chaos experiment | D: persistent versus memory-only checkpoints; memory-only state is lost on restart | Evaluation layer separate | Framework observability integrations separate | Durable state is an existing primitive. Test recovery instead of claiming to invent it. The requested durable-execution URL redirected to persistence documentation in retrieval. [S12](https://docs.langchain.com/oss/python/langgraph/persistence) |

### What the evidence supports

The sources establish considerable overlap and several integration boundaries. Agent Crash Test's inspected reporting list enumerates JSON and HTML but not Excel. Its inspected test-model document separates deterministic fixture checks from model-in-the-loop trajectory evaluation. DeepAgentLabs distinguishes observed errors from wrong answers and exposes configurable recovery semantics. These are reasons to investigate the proposed joint workflow; they do not prove that competitors lack it elsewhere or that users will choose Ram Lab.

Before committing to the full build, inspect the selected upstream release, run its credential-free demo in a disposable workspace, and check whether real process-death orchestration, claim evidence and workbook exporters are already provided. If the same joint workflow is available, contribute a focused exporter or workload pack instead. Validate usefulness with three technical reviewers using a short evidence bundle. Do not contact anyone automatically. Proceed only if reviewers can identify a recovery error or false completion claim more reliably with the bundle than with raw logs, or if the reproducible experiment itself provides a defensible portfolio contribution.

## 2. Build versus extend

| Option | Benefit | Main cost | Decision |
|---|---|---|---|
| Integrate Agent Crash Test JSON/bridge results | Reuses an explicit effect contract and logical/physical call distinction | Source-preview format drift; process lifecycle and model workload support need verification | Preferred starting point. Preserve upstream evidence IDs and capability flags; add namespaced fields rather than rewrite verdicts. |
| Attributed MIT fork | Allows a small missing lifecycle hook to be added directly | Larger maintenance and unclear ownership of original work | Only if the spike shows a necessary hook cannot be external. Retain copyright/license, pin commit and document changed files. |
| Compose agentic-chaos plus a new effect store | Broad fault and provider coverage | Much of the effect/restart bridge still needs designing | Secondary adapter after the first vertical slice. |
| Independent minimal harness | Complete control over the experiment and event schema | Recreates established functionality and risks scope growth | Fallback for a bounded local fixture only; document why integration failed. |

Licensed source reuse and independent feature implementation are separate tracks. Currently no competitor application code has been copied into this repository. Public README/license/spec inspection is research. If source is incorporated later, label its path, upstream commit, exact license and notices; do not call copied code clean-room work. New Ram Lab components are authored from its specifications. No competitor branding, proprietary assets, UI copy, or reviews become product content. A strict legal clean-room process has not been established by this research session.

## 3. Bounded MVP with real workloads

The UI's first choice is **Workload: App development / Homework-style assignment / Math**. The next controls select task, agent configuration, recovery policy, fault schedule and stress limits. The same harness runs actual tools and checks the resulting artifacts. Workload type is independent of fault type.

| Family | First two original task packs | Real work performed | Independent result oracle |
|---|---|---|---|
| App development | A1: build a small local task-list app from a written spec; A2: fix a supplied bug without breaking existing behavior | Agent reads/writes a disposable repo, runs locked build commands and browser tests, produces an actual app or patch | External acceptance tests and expected file/state invariants; app builds, required flows work, no unrelated file change. Screenshot is supplementary evidence, never the sole pass criterion. |
| Homework-style assignment | H1: answer questions from a provided history/science packet; H2: combine packet facts with a small data table and explain the calculation | Agent opens the packet, reads provided sources, calculates and creates a response with evidence locations | Packet-specific answer key and rubric, exact numeric checks, citation entailment and coverage. Open-ended writing quality is separately judged. These are original practice tasks, not school-account automation. |
| Math | M1: multi-step algebra with exact rational solutions; M2: units/geometry word problems with intermediate constraints | Agent reasons in its visible output, uses an allowed calculator or symbolic tool, validates its answer | Exact rational/symbolic equivalence, domain constraints, units and original-equation substitution. A wrong derivation with a coincidentally right answer is recorded separately. |

Six task templates keep scope bounded. Vary input instances through explicit generator seeds with saved answer keys. A small app task can still be a multi-minute real agent workload; no promise is made about completion time or model ability. Larger apps, open-web school research and competition-grade proof verification are later packs.

**Execution mode must be visible everywhere:** `live_agent`, `scripted_simulation`, `recorded_replay`, or `synthetic_example`. Only live_agent means a model actually interacted with tools during that run. A provider API or an explicitly selected installed local-model endpoint can supply it after the user controls access and spend. A deterministic fixture demo verifies harness mechanics; it does not establish agent reliability. The interview deliverable must include at least one genuinely executed live-agent experiment, with approval for inference obtained before running it.

Must-haves: one model/provider adapter; the three workload families; three recovery policies; six conditions below; child-process supervisor; immutable event/evidence capture; durable side-effect fixture; per-claim evidence; run comparison; local UI; reproducible CLI; bounded stress campaign; JSON/CSV/XLSX bundle; measured versus estimated usage/cost; a GitHub Pages read-only example viewer. Existing dependencies and adapters remain optional until tested.

Out of scope: general autonomous app building service, unbounded agent swarms, production outages, real payments/email/deployments, school logins or submissions, arbitrary process killing, hidden internal thoughts, universal hallucination detection, benchmark-leaderboard claims, multiplayer SaaS, hosted execution, model training, exhaustive framework support, and perfect cross-provider replay.

### Stress controls

Separate **resource stress** from **injected faults**. A campaign can vary task size (files, packet pages, reasoning steps), number of repeated jobs, input/output caps, concurrency and latency budgets. Resource observations include wall time, CPU time, peak resident memory, pending tool calls and queue length when supported. Mark unavailable OS metrics unavailable. Default to one worker; proposed configurable maximum four local workers, subject to the user's machine and measured resources. Hard-cap total run time, child memory where the OS supports enforcement, tool calls, retries, restarts and output bytes. Stop the campaign when limits are reached and retain partial evidence. Never stress the host indiscriminately or send load to third-party services without an explicit budget and permitted rate. Concurrency comparisons use identical resource caps and include host contention, not just model latency.

## 4. Architecture and local/public split

Proposed stack: TypeScript on a pinned supported Node LTS, one local supervisor/CLI, SQLite for durable metadata, content-addressed local files for raw evidence, and a React/Vite static viewer. Reuse the selected upstream contract engine through a versioned file adapter. Choose and license-check exact database/XLSX/browser-test packages at the post-approval dependency spike. No account, Postgres, Redis or cloud service is needed for the local harness. The current planning workbook uses the available artifact runtime; that does not choose the application's export library.

```text
Local CLI / local run controls
             |
     Experiment supervisor ---------------- Observer / effect fixture
       |          |                               |
       |      fault schedule                 durable business state
       |          |
    agent worker process ---- tool gateway ------ tools / model adapter
       |                        |
       +---- observable events -+---- evidence writer / SQLite journal
                                         |
                         evaluators -> comparison -> JSON/CSV/XLSX
                                         |
                              static trace bundle + viewer
                                         |
                       GitHub Pages: read-only sanitized examples
```

The supervisor survives the worker it kills. The business-effect service and observer are outside that worker too, so a new worker can inspect committed state. The supervisor logs process exit using an owned process handle, exit status and incarnation ID, rather than trusting the worker to emit its own death event. A Windows process termination is recorded as that operation; do not label it SIGKILL. Linux signal tests are a separate platform result. A Windows Job Object or equivalent scoped process-tree mechanism is investigated during the spike. No arbitrary PID input.

GitHub Pages serves static files. It cannot host the Node supervisor, SQLite service or OS process controls. The Pages build uses a repository base path `/ram-lab/`, sanitizes bundles, uses only static assets, and never embeds API credentials. Its replay viewer has no live execution buttons. The local viewer can read local run bundles; optional run actions call a loopback-only endpoint with a session nonce and origin validation. No silent connection from the public site to localhost. See [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages) for the hosting boundary.

### Data ownership and entities

| Entity | Key and relationships | Required constraints |
|---|---|---|
| Experiment | experiment_id; references workload/version, policy, schedule and agent config hashes | Immutable configuration after scheduling; no secrets in config |
| Run | run_id; belongs to experiment; baseline_pair_id and task_instance_id | Unique run ID; execution mode; lifecycle status separate from correctness |
| Process incarnation | process_id; belongs to run; parent incarnation and checkpoint | Unique incarnation; boot identity; owned handle; restart ordinal |
| Event | event_id; run_id, trace/span/parent IDs, process_id | Unique producer+sequence; append-only; schema version; causal links |
| Tool attempt | attempt_id; logical_operation_id, step_id, run_id | Physical attempt distinct from logical intent; stable idempotency key |
| Fault decision | fault_id and decision_id; schedule item, target operation, observed event | Scheduled, eligible, fired and observed are different fields |
| Checkpoint | checkpoint_id; run_id, sequence boundary, state hash | Complete snapshot with durable commit receipt; prompt/model/tool versions |
| Effect observation | observation_id; operation key, authoritative snapshot IDs | Before/after version, committed effect IDs, observer status and freshness |
| Claim | claim_id; response artifact hash + byte offsets, run_id and step_id | Exact text retained; extraction version; no silent dedup across runs |
| Claim evidence link | claim_id + evidence_id + relation + scorer_version | Many-to-many support/contradict/insufficient; evidence location and scope |
| Evaluation | evaluation_id; target run/claim/contract; rubric hash | Append-only revisions; evaluator identity/type; uncertainty/abstention |
| Usage/cost | usage_id; provider request ID, attempt_id, price snapshot | Nullable usage; unit categories; no duplicated provider charge |
| Artifact | evidence_id; content hash, relative URI, media type, size | Integrity check, redaction state and access level; missing != empty |

Keep foreign keys explicit, index run_id and foreign-key columns, and use unique constraints for provider request identity and operation keys where appropriate. Use integer microdollars for cost arithmetic, integer token counts and integer monotonic nanoseconds where available. Store UTC timestamps and display the selected timezone. Proposed tables are design contracts, not executed migrations.

### Event envelope v1: required design

Every event contains `schema_version`, `event_id`, `experiment_id`, `run_id`, `event_type`, `producer_id`, `producer_seq`, `process_incarnation_id`, `timestamp_utc`, `monotonic_ns` if available, `clock_domain`, `observed_by`, `knowledge_class` (recorded/inferred/judgment), and `payload`. Optional correlation: `trace_id`, `span_id`, `parent_span_id`, `caused_by_event_ids`, `task_id`, `step_id`, `logical_operation_id`, `attempt_id`, `fault_id`, `checkpoint_id`, `evidence_ids`. Unknown values are null with a reason; do not fabricate timestamps or token counts.

Payloads are a discriminated union. Lifecycle: run/step/process started, ended, lost or timed_out. Tool: request, result, error, delivery_lost. Fault: scheduled, skipped, injected, observed. Recovery: checkpoint_committed, worker_exit_observed, restart_started, state_loaded, reconciliation_started, reconciliation_resolved, recovery_verified, recovery_failed, recovery_unknown. Evaluation: claim_extracted, claim_evaluated, contract_evaluated. Resource: usage_reported, cost_estimated, resource_sample, budget_exhausted. Log overflow or missing sequence produces evidence_gap, never an assumed healthy trace.

Example, a design illustration only:

```json
{
  "schema_version": "1.0",
  "event_id": "example-E008",
  "experiment_id": "example-X1",
  "run_id": "example-R1",
  "event_type": "effect.observed",
  "producer_id": "observer",
  "producer_seq": 8,
  "process_incarnation_id": "observer-1",
  "timestamp_utc": "2026-10-28T01:00:02.000Z",
  "monotonic_ns": "2000000000",
  "clock_domain": "supervisor-boot-1",
  "observed_by": "durable-state-observer",
  "knowledge_class": "recorded",
  "logical_operation_id": "create-item-17",
  "attempt_id": "attempt-1",
  "evidence_ids": ["example-V003"],
  "payload": {
    "operation_key": "example-R1/create-item-17",
    "observer_status": "ok",
    "state_version": 4,
    "committed_effect_ids": ["item-17"]
  }
}
```

Ordering uses producer sequence and explicit causality, not timestamp sorting alone. A process monotonic clock resets on restart; subtract only times within a verified shared domain. Supervisor-observed boundaries provide comparable cross-process durations. Concurrent span durations do not sum to run wall time. Preserve unfinished spans and right-censor them at the observation boundary.

Raw evidence records include ID, SHA-256, relative location, byte range/JSON Pointer/page location, creation time, producer, source version, original versus delivered view, redaction provenance and retention state. A checksum detects later byte changes; it does not prove the event was truthful. Redacted artifacts get a new hash and a mapping to the retained original ID. Default private run storage stays local; public evidence is synthetic or explicitly sanitized and reviewed.

## 5. Fault and recovery semantics

Six initial experimental conditions: clean baseline plus five fault conditions. Each schedule identifies semantic step, operation key, occurrence number, injection boundary, parameters, seed, maximum firings, and schedule version. Fault metadata is available to the supervisor/evaluator but hidden from the agent unless its task normally exposes that information.

| Condition | Exact injection | What is measured | Recovery requirement |
|---|---|---|---|
| C0 clean | Same instrumentation, no injection | Instrumentation baseline and normal errors | No recovery claim when nothing failed |
| C1 transient timeout/rate limit | One selected tool/model call fails before a known commit; model-transport and tool variants separately labeled | Detect/retry/backoff; actual elapsed time and bounded attempts | Retry only if operation is safe and budget permits; count SDK retries too when observable |
| C2 malformed or corrupted output | Save original tool result, deliver a mutated result with versioned mutation | Parser behavior; incorrect versus unsupported downstream claims | Validate shape/content, obtain independent evidence or abstain |
| C3 worker death before commit | Supervisor terminates its owned worker at an acknowledged pre-commit barrier | Exit observation, checkpoint durability and restart | New incarnation loads committed state; oracle confirms no prior effect before reissue |
| C4 worker death after commit before result delivery | Effect service commits durably and notifies supervisor; supervisor kills worker before its delivery/checkpoint acknowledgement | The ambiguous-outcome window; physical attempts and durable effects | Query by stable operation key, reuse committed result, never infer non-commit from a timeout |
| C5 stale checkpoint/read | Restore a versioned earlier checkpoint or return a stale read with retained true snapshot | Repeated action, state mismatch, claim errors | Detect version conflict, reconcile current state, or report unknown and stop |

Drop-after-commit without worker death is a useful separate micro-test; never label it a process crash. Resource saturation is a separate stress axis, not another synonym for malformed output. Avoid compound faults until single-fault semantics pass.

**Task status and harness status are separate.** A run may finish successfully at the harness level but produce a wrong app/math answer. A worker may restart cleanly while still creating two items. `recovery_verified` requires an observed injected failure, subsequent usable progress, final task invariants and authoritative effect checks. A nice final answer or absence of an exception is insufficient. Baseline failures stay in the dataset.

Three policies: P0 bounded naive retry; P1 durable checkpoint resume with bounded retry; P2 checkpoint resume plus stable operation keys, fresh outcome reconciliation and conflict checks. Keep model, prompt, tools, retry caps and budgets equal when isolating policy. Record any unavoidable policy-specific prompt differences.

The fixture's business database enforces uniqueness on `(run namespace, operation key)` and stores the canonical request hash plus result. Same key + same request returns the existing result. Same key + different request is a conflict. A completed effect and its idempotency record commit in one fixture transaction. This permits an exactly-once **effect invariant within this fixture**, while attempts may be at least once. It does not guarantee exactly-once effects across arbitrary external APIs. When an external service cannot answer by key, recovery is `unknown` and non-idempotent writes stop.

Checkpoint state includes workflow position, visible message references, pending operation keys, tool schema/version, task/environment hashes and last durable event boundary. Never place paid credentials in it. Commit to a temp snapshot and durable atomic replacement or a database transaction; acknowledge only after persistence requirements are met. A checksum alone is not durability. Lock/fence a run so two incarnations cannot resume simultaneously; invalid or missing state yields a visible failure, not a new silent run. Separate worker-crash, tool-process-crash, supervisor-crash and power-loss guarantees. MVP covers worker crash while supervisor and effect service survive; power loss and killing the whole host are out of scope.

Recovery timing exposes fault command time, fault observation time, detection, restart start, state loaded, reconciliation complete, first verified progress and final recovery verification. Report detection delay, restart delay, reconciliation duration, time to usable progress and time to verified final result separately. Runs that never recover are right-censored or failed under the predefined deadline, not excluded from average recovery time without a count.

## 6. Claims, hallucinations and observable decisions

Record tool requests/responses, returned error codes, visible next action, selected retry/fallback, checkpoint load and any agent-provided rationale or exposed reasoning summary. Store rationale verbatim as agent-provided content with its event ID. It can be inaccurate, post-hoc or absent. It is not a record of hidden internal thoughts and is never the oracle for what happened.

Claims are atomic, checkable assertions extracted from final output and selected intermediate visible responses. Examples: "The app's tests passed", "I created exactly one item", "the packet says X", "x = 3", and "the first call did not commit". Keep exact source offsets alongside normalized subject/predicate/object, relevant time and target. Split compound statements consistently. Do not count code strings, quoted opponent claims, questions or preferences as asserted facts. Audit extractor omissions with human review.

Use two axes rather than collapse everything into a hallucination percentage:

| Axis | Allowed values | Meaning |
|---|---|---|
| Truth relative to specified oracle | supported, contradicted, unresolved, not_applicable | Evidence supports or conflicts with the assertion at its time/target, or the evaluator cannot decide |
| Grounding in evidence actually available to agent | supported, unsupported, unavailable, not_applicable | A true claim can still be unsupported by what the agent saw; a faithful report of a corrupted tool result can be false against the authoritative state |

Record evidence relation per link: supports, contradicts, insufficient, or source_conflict. A known false claim is contradicted, with the contradiction cited. Unsupported means available references do not establish it; it does not prove falsehood. Unverifiable/unresolved means the oracle is missing, ambiguous, stale or beyond scope. A missing observation never proves that no effect occurred. Conflicting sources remain visible. Use a designated authority/version for time-dependent facts, not whichever passage agrees with the model.

Each judgment includes evaluator kind/version, rubric hash, applicable evidence IDs and exact locations, scope, confidence category with reasons, abstention reason, reviewer/adjudication state, and alternatives when disputed. An optional numeric model confidence is stored as an uncalibrated score unless calibrated on held-out labels. Keep automated proposals and adjudicated labels separately; never overwrite historical labels. Deterministic numeric/effect/build checks have priority within their explicitly defined scope; subjective rubric checks can abstain. Do not promote all test failures to hallucinations: a parser exception has no factual claim, and an incorrect calculation is an incorrect mathematical result even when a broader hallucination taxonomy also labels it.

Causal attribution requires more than adjacency. Show first observed discrepancy and explicit causal links. A paired intervention can support a fault contribution, but one run cannot establish that the fault caused every later mistake. Keep injected ground truth separate from evaluator diagnosis so attribution accuracy can be measured without leaking the answer to the scorer.

### Denominators and uncertainty

| Metric | Numerator / denominator | Required accompanying counts |
|---|---|---|
| Task success | task-oracle passes / all started eligible task runs | success, failure, timeout, aborted, inconclusive; pre-start invalid configurations separate |
| Verified recovery | runs meeting full recovery contract / eligible runs with an observed injected failure | fired, observed, skipped/unreached, censored and unknown |
| Contradicted-claim rate | contradicted / adjudicated supported + contradicted claims | unresolved, excluded, total extracted; never count unresolved as correct |
| Unsupported-claim rate | grounding-unsupported / claims with grounding adjudication | unavailable grounding and extractor coverage |
| Claim coverage | claims with supported/contradicted truth adjudication / all eligible extracted claims | extractor/manual sample count and exclusions |
| Duplicate-effect rate | logical writes with more committed effects than allowed / logical writes with complete authoritative observations | extra physical attempts and deduplicated attempts separately |
| Fault activation | actual firings / eligible scheduled opportunities | scheduled count and unreachable/skipped targets |
| Retry overhead | extra physical attempts relative to matched baseline / baseline attempts | SDK-observable coverage and unknown hidden retry counts |

No observed rates exist yet. Workbook example rates are calculated solely from labeled synthetic rows. Always show x/n. A zero denominator is unavailable, never 0%. Report Wilson intervals for genuinely independent binomial samples; for clustered task repetitions, use a prespecified paired cluster bootstrap and report its seed and cluster count. Small samples get wide uncertainty, not extra decimal places. Summaries at claim, run and task levels answer different questions and must not be averaged interchangeably. Report micro and per-task macro rates with explicit definitions if both are needed.

## 7. Usage, cost and evidence completeness

Capture provider request IDs, attempt IDs, model/version, input/output/cached/reasoning unit categories, token count source, request start/end, transport status and usage availability. Provider-reported usage is observed usage, not an independently audited invoice. Dollar cost is measured only when an actual provider charge/cost record is available; otherwise it is a price-based estimate with a dated price snapshot, currency, units, source URL and any discounts. Never label token count times list price billed cost.

For mutually exclusive usage categories, estimated cost = sum(units × applicable unit price) plus applicable request/tool fees. Reasoning tokens may already be included in output; cached tokens may be a subset of input. Normalize provider categories before summing to avoid double billing. Record the normalization version. A timeout can still consume tokens and money. Missing usage is unknown, not zero. Preserve known subtotal, count of unknown-cost requests and completeness. A partial total must say partial. Keep evaluator inference, embeddings, tools and agent inference separate. Do not add them twice through both call and run totals.

Durations come from recorded boundaries; missing endings remain missing. Token estimates from a tokenizer and cost estimates from prices have distinct labels. No numeric provider prices are assumed in this plan. User approval is required before paid inference. Budget estimates are calculated after adapter selection: tasks × policies × conditions × repetitions × expected calls × observed pilot tokens per call × price, plus evaluator/tool spend and a reserve. Stop on the explicit approved budget, with in-flight commitments accounted for.

## 8. UI and CLI design

Six original screens; no competitor layout or assets copied.

| ID | Screen and content | Important states |
|---|---|---|
| S01 | Experiments: workload, task, live/simulation mode, agent, recovery policy, fault/stress limits and budget | invalid schedule, missing model access, read-only hosted mode, ready |
| S02 | Runs: baseline/fault pairs, task/harness outcomes, usage completeness and x/n summaries | empty, running, failed, censored, partial evidence |
| S03 | Run timeline: process lanes, steps, attempts, faults, checkpoints, visible decisions/rationale | no rationale, unfinished span, new incarnation, evidence gap |
| S04 | Recovery and effects: before/after state, operation key, attempts/effects and reconciliation | verified, violated, unknown, stale oracle, missing checkpoint |
| S05 | Claims: exact text, truth and grounding labels, supporting/contradicting evidence, scorer uncertainty | unresolved, source conflict, pending review, evaluator disagreement |
| S06 | Compare/export: matched policies and workloads, uncertainty, resource/cost overhead, downloadable bundle | incomparable configs, partial cost, missing pairs, synthetic warning |

F01 configure and run: S01 -> S02 -> S03. F02 investigate recovery: S03 -> S04 -> evidence drawer. F03 inspect a completion claim: S03 -> S05 -> evidence drawer. F04 compare and export: S02 -> S06. Evidence clicks must resolve the exact ID/hash/location or display missing evidence. No silent nearest-match substitution.

The shared evidence drawer shows recorded facts, inferred behavior and evaluator judgment as labeled rows, not only colors. Text badge plus icon identifies run mode. Keyboard navigation, focus visibility, legible status contrast, reduced motion, responsive tables and non-color status distinctions are acceptance requirements. A proposed neutral white/dark-slate palette and one restrained accent are sufficient; no brand-clearance claim is made for the working name Ram Lab.

Proposed CLI grammar, **not implemented commands**:

```text
ramlab doctor
ramlab tasks list --family app|homework|math
ramlab plan experiments/app-recovery.json
ramlab run experiments/app-recovery.json --mode live-agent --budget <approved-limit>
ramlab stress experiments/math-stress.json --concurrency 1 --repeat 10
ramlab replay runs/<run-id>/bundle.json
ramlab compare runs/<baseline> runs/<faulted>
ramlab export runs/<run-id> --formats json,csv,xlsx
ramlab verify runs/<run-id>/bundle.json
```

The validation-only `plan` command must not execute target tools or paid calls. `doctor` reports capabilities without opening accounts. Comparison refuses to silently pair different task instances or oracle versions. The local API, if needed: GET /runs, GET /runs/:id, GET /runs/:id/events, GET /evidence/:id, POST /experiments/validate, POST /runs, POST /runs/:id/stop and POST /exports. Only local session-authorized controls can mutate; static Pages exposes none of these endpoints.

## 9. Excel reporting specification

See EXCEL-SPEC.md for the field dictionary, formulas, joins and validation. It defines individual runs, wall-clock and step timelines, attempts, faults/recovery, effect reconciliation, exact claims, evidence, usage/cost, paired comparisons and evaluator uncertainty. The sample workbook is a design illustration with explicitly synthetic data, not a real stress test or an evaluation of any model. Public exports retain evidence identity and disclose redaction. Raw JSON/binaries live beside the workbook; Excel cell limits must not silently truncate evidence.

## 10. Experimental design

Prespecify one main question: does reconciliation reduce duplicate/missing effects and false completion claims after an observed worker crash, compared with bounded retry and checkpoint-only resume, within these six task templates? Resource-stress robustness is a separate question. Do not rank models using a mix of different faults, prompts and hardware.

1. Validate oracles using known-good and intentionally broken outputs before running a model. Validate fault barriers and durable effects with a deterministic worker. Test the harness without claiming agent results.
2. Create six original task templates, two per family. Save generated instance, answer key, allowed tools, expected effects, locked test suite, limits and hashes. Do not give hidden acceptance answers to the agent. Test math equivalence rather than string matching; manually audit source citations and open-ended rubric items.
3. Establish an instrumented clean baseline for every task, agent and policy. Add a no-instrumentation microbenchmark only to estimate harness overhead. Keep it distinct from task quality comparisons.
4. Use three policies × six conditions × six task templates × ten instance/schedule seeds: 1,080 planned offline harness runs. These are proposed design counts, not completed experiments. Repeating a deterministic simulation does not yield statistical evidence about live LLMs.
5. After inference approval, start a smaller live pilot: six tasks × three policies × three conditions (clean, pre-commit death, post-commit death) × five repetitions = 270 proposed runs. Reduce the pilot before starting if its budget exceeds the approved cap. Five repetitions is a feasibility pilot, not a powered reliability claim. Freeze a confirmatory sample size after variance and failure frequency are estimated, using a declared minimum effect of practical interest and budget.
6. Pair task instances, model settings and semantic fault schedules across policies. Randomize policy order within task blocks to reduce service/hardware drift. Record model/provider fingerprint and time; a seed does not guarantee provider determinism. If a semantic target is never reached, record skipped/unreached instead of moving the fault to another arbitrary call.
7. Run a separate stress ladder: one, two and four concurrent local workers only when resource caps allow, and small/medium task inputs with explicit file/page/step counts. Use the same tasks/policies and compare throughput, tail latency, timeouts, resource use, correctness and recovery. Concurrency is a host condition; trials on one computer do not generalize to all machines.
8. Primary outputs: task success x/n, duplicate/missing effects x/n, verified recovery x/n, contradicted/unsupported claims with coverage, and paired wall-time/token/cost differences. Report family-specific results before pooled results. Include failures, censored runs and unknowns. No best-run selection.
9. For task effects, use paired differences and task/instance cluster bootstrap intervals with fixed bootstrap seed. With only a few templates, emphasize individual task results and limited generalization. Independent-run Wilson intervals are descriptive where the assumptions actually hold. A p95 from a tiny pilot is unstable; show sorted samples or quantiles with n and uncertainty instead.
10. Keep automated and human labels, sample extraction errors, double-label a prespecified subset, report disagreement and adjudication. Judge self-reports are not calibrated confidence. Evaluator models remain separate from task agents; control fault-ground-truth leakage.

Reproduction bundle: config/schema version, source commit and dirty flag, dependency lockfile digest, operating system/runtime, CPU/memory limits, task/source/oracle hashes, model settings, provider fingerprint, fault schedule and seeds, attempt log, checkpoints, original/delivered artifacts, normalized events, evaluations, cost price snapshot, export tool version and a manifest of hashes. Replay reproduces recorded evidence and evaluation, not the exact behavior of a remote stochastic model. Remote re-execution is a new run.

## 11. Staged implementation after approval

Time estimates below are provisional effort ranges, not a delivery promise.

| Stage | Deliverable | Exit gate |
|---|---|---|
| 0, now | Sourced plan, workflow verification, public repo, documentation site, workbook illustration | Reviewable artifacts; no application code |
| 1, approximately 1–2 focused days | Pin upstream, inspect license/dependencies, execute credential-free demo in isolation, verify JSON adapter and Windows process lifecycle | Document integration decision with one observed effect contract; no unapproved provider calls |
| 2, approximately 2–4 days | Event journal, evidence bundle, actual owned-worker death/restart and durable effect fixture | C3/C4 barriers demonstrated; missing/corrupt checkpoint fails visibly; repeated operation cannot silently duplicate |
| 3, approximately 3–5 days | Three workload families, actual model adapter, three recovery policies and bounded stress controls | At least one app, homework-style and math task executed by a real agent after access/spend approval; independent oracles attached |
| 4, approximately 2–4 days | Claims and grounding, comparisons and versioned evaluations | Known-false/unsupported/unverifiable examples correctly separated; scorer disagreement retained |
| 5, approximately 2–4 days | Original viewer, CLI demo, forensic workbook exporter and static example deployment | Every displayed conclusion traces to evidence; all export formulas/links inspected; public data review complete |
| 6, budget dependent | Frozen experiment campaign, interview recording and write-up | Preregistered settings, complete denominators, uncertainty, limitations and reproduction |

Commit policy: commit immediately after each discrete completed change and its relevant check. A background-color edit is one commit; a font edit is another. Do not batch unrelated visual or behavioral changes. Keep compilation and its necessary associated edits together only when they constitute one indivisible change. Do not manufacture empty commits. Commit message states the specific change and validation. Never commit credentials, private traces or model API keys. Work on this new repository only; existing profile and four pins are outside scope.

## 12. Interview demonstration and acceptance

Target a five-minute walkthrough. Show the selected workload and a clean result first. For the app pack, create a task item or save a document through the durable fixture. Kill the actual agent worker after commit but before acknowledgement. Show the supervisor's exit evidence and new process incarnation. Compare naive retry producing an intentional duplicate against reconciliation finding the prior effect and continuing. Open the agent's completion claim and the independent state/test evidence. Switch to a math or homework pack to show the same harness with a different oracle. Export/open the workbook and follow one claim to its raw evidence. The Pages version can replay a sanitized real run or labeled synthetic sample; it cannot run the experiment.

Acceptance criteria:

- A public repo and reachable GitHub Pages documentation exist; no claim that the application is built during Stage 0.
- The exact workflow invocation is `/autopilot fullreplicate`; explicit reading/command-reader verification is distinguished from native host discovery.
- All three workload families run actual task tools; live model use is visibly distinguished from simulations/replay. At least one independently checked live-agent run per family is required before advertising real-case support.
- Process-crash demos include supervisor-owned termination, OS-observed exit, a changed incarnation and durable state observed outside the killed worker. Raising a timeout exception fails this criterion.
- C4 proves one durable effect under P2 and exposes the intentionally unsafe alternative. Attempts and effects have different counts. Missing or stale oracle evidence yields unknown/inconclusive.
- Every retry/restart/fault/checkpoint has a stable ID and a bounded budget; event loss is surfaced. Timings show clock source and censoring.
- Claims have exact source locations, supporting/contradicting evidence, truth/grounding labels and scorer uncertainty. Hidden thoughts are never claimed.
- App tests, packet rubrics and math validators are independent of the agent's own declaration. Incorrect results remain failures even if the process recovers.
- Comparison uses matched task/config keys; rates show x/n, unresolved counts and method-appropriate uncertainty. Cost completeness and estimate/billed status remain visible.
- JSON and workbook agree on row counts, IDs, denominators, known cost subtotals and recovery durations. Evidence paths/hashes verify or show a specific failure.
- Offline CLI reproduction needs no account; real-model re-execution needs explicitly selected access and budget. A clean Windows run is tested; other-platform claims require their own evidence.
- Each discrete change has its own commit; no changes touch the GitHub profile or four pinned repositories.

## 13. Risks and decisions still open

1. **Differentiation may collapse.** The closest tool may already support the joint experiment. Stage 1 can reduce this to an upstream exporter/workload contribution.
2. **Task scope.** App creation is much more expensive than simple math. Keep six small templates and expose per-family limits. Do not expand to arbitrary user tasks until core evidence is sound.
3. **Real-agent access.** Provider/local-model choice and inference budget remain user-controlled. No live agent reliability has been measured yet.
4. **Windows lifecycle isolation.** Validate process-tree cleanup and durable barriers. Worker death is narrower than whole-system crash or power loss.
5. **Observer correctness.** A corrupt fixture can give a false proof. Independently seed known state violations and test the observer's negative/unknown cases.
6. **Evaluation reliability.** Claim extraction, ambiguous wording and source conflict create uncertainty. Manual adjudication and explicit coverage are necessary.
7. **Costs and latency.** Unknown timed-out requests can understate spend; concurrency can confound model performance. Retain partials and host metrics.
8. **Public artifacts.** Real prompts, file paths and tool outputs can reveal private information. Publish only reviewed, redacted bundles with explicit permission; keep raw runs local.
9. **Upstream stability/licensing.** Pin versions and retain notices. Dataset, model and enterprise terms are separate from a repository's general license.
10. **Naming and licensing.** Ram Lab is a working name; no trademark/domain clearance claimed. Choose the new code's license before application release. Public visibility alone does not confer a reuse license.

Plan approval authorizes the selected next implementation stage only as agreed. Authentication, paid inference and later production integrations remain controlled by the user. The original planning-only restriction is still active.
