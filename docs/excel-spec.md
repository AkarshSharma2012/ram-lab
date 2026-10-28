# Ram Lab forensic Excel workbook specification

Version 1 design, October 27, 2026. This specification is a plan. The accompanying workbook is a synthetic illustration. It contains no measured agent benchmark results. Intended readers: the developer investigating a run and a technical interviewer comparing recovery behavior. Target: ordinary desktop Excel with macro-free XLSX, plus a raw evidence bundle for records too large for cells.

## Contract and layout

Canonical source is a versioned JSON run bundle, not the workbook. The exporter validates it, builds normalized tables, calculates summaries and emits an export manifest. A workbook is an auditable view, not the sole raw-data store. One row has one documented grain. Foreign keys are strings and remain strings; dates, durations, counts and costs are typed values with units. Raw source data never reads formulas from a summary.

Sheet order: Overview, Compare, Runs, Timeline, Calls, Recovery, Effects, Claims, Evidence, Usage, Dictionary. Eleven sheets serve distinct grains and investigation needs. A terminal QA summary may be added to Dictionary; no metric reads a QA verdict. No hidden sheets, macros, external data connections, circular formulas, arbitrary weighted reliability scores or hidden reasoning fields. Table filters and frozen headers identify large tables; freeze ID columns when horizontal scrolling requires it. Use text labels plus restrained exception colors. Preserve source IDs through sorting. Header rows are unmerged and each column contains one variable. Summary formulas link to owning tables, not copied hardcoded totals.

Every sheet displays the mode of its data: live_agent, scripted_simulation, recorded_replay or synthetic_example. Exports with mixed modes must filter/split results and must not pool them. A static sample must never look like an actual completed experiment.

## Sheet dictionary

### Overview: reader summary

Scope: experiment/config digest, export time/version, task families, run modes, selected population and incomplete evidence warning. Show counts of started runs, task passes/failures/timeouts/inconclusive, injected/observed failures, verified/failed/unknown recovery, adjudicated versus unresolved claims, and known/unknown spend. Show x/n beside every rate, with method and uncertainty when meaningful. Synthetic examples use illustrative counts, not empirical confidence claims. Provide internal hyperlinks to selected run, first divergence, recovery, claim and evidence rows. A comparison chart may show measured wall time per policy, with zero origin and units; it does not imply statistical significance.

### Compare: one matched pair or stratum per row

Fields: comparison_id, task_instance_id, family, task/oracle/config versions, baseline_run_id, candidate_run_id, policy pair, fault schedule hash, matching_status/reason, baseline/candidate task status, fault eligibility/observed flags, baseline/candidate wall_ms, paired_delta_ms, baseline/candidate physical_calls, paired_retry_overhead, duplicate/missing_effects, known_agent_cost_usd, unknown_cost_calls, cost_basis, evaluated_claims, contradicted_claims, unsupported_grounding, unresolved_claims, coverage, and effect-violation evidence IDs.

Pairs must match task instance, model settings, oracle, tools, resource caps and scheduled semantic boundary. Policy can differ by design and is recorded. Refuse invalid joins; never join on display names or row order. Stratified aggregate tables show family, condition, policy, x, n, missing/censored counts, interval method and bounds, bootstrap seed and cluster unit. Do not average claim percentages across runs and call that a micro rate. Sorted samples or median/IQR are preferable to unstable p95 estimates for tiny n.

### Runs: one started run per row

Identity: experiment_id, run_id, baseline_pair_id, task_instance_id, family, task_version, source_commit, dirty_flag, dependency_digest, config_hash, agent_id/model/provider/fingerprint, policy, execution_mode, schedule_hash, instance_seed and fault_seed.

Lifecycle: scheduled_utc, started_utc, ended_utc, supervisor_clock_domain, wall_ms, queue_ms, process_count, steps_started/ended, harness_status, task_status, oracle_id/version, stop_reason, censoring_status and observation_deadline. Never encode all of this as one success boolean.

Results: logical_operations, physical_attempts, known_effects, extra_effects, missing_effects, unobserved_operations, fault_eligible/fired/observed counts, recovery_status, first_divergence_event_id, claims_extracted/eligible/adjudicated/contradicted/unresolved, grounding_unsupported, known_tokens, unknown_usage_requests, known_cost, unknown_cost_requests, cost_basis and evidence_manifest_id. Running or missing-ending runs retain blank durations plus a reason.

### Timeline: one event/span boundary per row

event_id, run_id, producer_id/sequence, process_incarnation_id, clock_domain, timestamp_utc, supervisor_elapsed_ms, event_type, step_id, span_id/parent_span_id, logical_operation_id, attempt_id, fault_id, checkpoint_id, caused_by_event_ids, actor, observable_decision, rationale_artifact_id, knowledge_class and evidence_ids. Rationale is optional and marked agent-provided. Do not call it internal thought.

A duration view joins paired start/end records by span ID; required columns are start/end event IDs, start/end elapsed_ms, duration_ms, inclusive/exclusive scope and censoring. Cross-process timings use a common supervisor boundary; if clocks cannot be aligned, do not manufacture an ordering or duration. Parent and child durations overlap. Gantt-style views are derived from these values; no sum of all step durations as end-to-end latency.

### Calls: one physical tool/model attempt per row

attempt_id, run_id, step_id, logical_operation_id, retry_ordinal, provider_request_id, tool_name/schema_version, idempotency_key, request_evidence_id/hash, original_response_evidence_id/hash, delivered_response_evidence_id/hash, started/ended event IDs and elapsed_ms, status/error_code, provider_latency_ms, total_attempt_ms, injected_delay_ms, scheduled_backoff_ms, observed_backoff_ms, SDK_retry_visibility, side_effect_class, effect_receipt_id, and outcome_known. Store full request/response in Evidence or sidecars, never truncate silently. A timeout may have a committed effect and unknown cost.

Retries are extra attempts linked to the same logical operation, not all repeated text or identical tool names. Checkpoint replay that does not reissue a call is a different event. Duplicate delivery, repeated physical attempts and duplicate durable effects get separate columns.

### Recovery: one fault/recovery episode per row

episode_id, run_id, fault_id, scheduled_target, seed, mutation_version, eligibility, scheduled_boundary, actual_boundary, original/mutated evidence IDs, scheduled/fired/observed flags, skipped_reason, exit_observed_event_id, old/new incarnation IDs, checkpoint_id/digest, loaded_state_version, oracle_version, detection/restart/reconciliation/progress/verification event IDs and elapsed_ms, deadline_ms, censoring, status, stop_reason and contract/evidence IDs.

Derived durations: detection_ms = detection - fault command; restart_ms = new process ready - restart start; reconcile_ms = reconciliation end - start; progress_ms = first verified progress - fault observed; verified_recovery_ms = final recovery verified - fault observed. All require comparable clocks and endpoints. A never-recovered episode has no finite verified duration. Show failed and unknown/censored counts next to recovered-only medians.

### Effects: one logical side-effect operation per row

operation_id, run_id, task_target_id, side_effect_type, operation_key, canonical_request_hash, allowed_cardinality, physical_attempt_count, deduplicated_attempt_count, observer_status, observer_freshness/version, before_evidence_id, after_evidence_id, receipt_evidence_id, committed_effect_ids, observed_cardinality, missing_effect_count, duplicate_effect_count, unrelated_mutation_count, reconciliation_action, truth_scope, contract_status and contract_version. Blank observation is unknown, not cardinality zero. Exactly-once is an effect invariant only for the stated fixture/service.

### Claims: one extracted atomic claim per row

claim_id, run_id, step_id, response_artifact_id/hash, start_byte, end_byte, exact_text, normalized_claim, asserted_target/time, extraction_method/version, eligibility, exclusion_reason, truth_label, grounding_label, support_evidence_ids, contradiction_evidence_ids, unavailable/conflicting_evidence_ids, evidence_locations, evaluator_kind/version, rubric_hash, judgment_id, confidence_category/reason, raw_model_confidence (optional, uncalibrated), abstention_reason, reviewer_label, adjudication_status and adjudicated_label/version.

Keep link records in the JSON bundle when there are many per claim. Workbook cells can list IDs and hyperlink to the first corresponding Evidence row; the complete list is preserved. Contradicted means cited evidence conflicts with the claim. Unsupported grounding does not prove falsehood. Unverifiable/unresolved claims stay outside the binary truth denominator and in coverage counts. Any model-judge scores remain estimates or judgments, never recorded facts.

### Evidence: one immutable artifact per row

evidence_id, run_id, producing_event_id, artifact_kind, media_type, byte_length, sha256, relative_uri, JSON_pointer/byte_range/page, source/version, captured_utc, original_or_delivered, redaction_status, supersedes/original_evidence_id, knowledge_class, access_state, short_preview and full_text_if_small. IDs and locations link conclusions back to raw observations. Verify digest on export. A hash does not certify source truth. Treat spreadsheet formula-shaped text as text to prevent formula injection; only exporter-authored formula cells execute.

Do not exceed Excel's cell/row limits silently. Large bodies stay in bounded sidecars with ID/hash/size and a truncation flag on the preview. Split a large event table into documented partitions or export CSV/JSONL with manifest row counts. Workbook/sidecar paths are relative within a portable directory/ZIP, not personal absolute paths. File hyperlinks may prompt Excel security; missing links show an explicit failure in the local viewer. Never assert that a PNG preview proves native Excel hyperlink behavior.

### Usage: one provider request or evaluator/tool charge record per row

usage_id, run_id, attempt_id, provider_request_id, actor_kind (agent/evaluator/tool), model/version, usage_source (provider_reported/tokenizer_estimated/unavailable/synthetic), input_uncached_tokens, input_cached_tokens, output_tokens, reasoning_subset_tokens, normalization_version, unknown_usage_reason, price_snapshot_id/effective_utc/source_url/currency, unit prices, request_fee, estimated_cost_usd, provider_reported_cost_usd, invoice_charge_id, chosen_cost_basis, known_subtotal and completeness. Cost records match provider request IDs; a run total never adds both estimate and actual for the same charge. Missing usage remains blank with a reason, even when another request has zero tokens.

### Dictionary: definitions and terminal validation

List field, grain, type, units, nullable rule, enum or accepted range, source/derivation, owning sheet, and metric inclusion. Include mode definitions, scorer uncertainty, row capacities, export version and plan/source references. Terminal checks: duplicate IDs, orphan foreign keys, missing evidence/hash mismatch, unequal joins, start/end order, repeated provider charge, unavailable cost count, rate numerator/denominator and row count reconciliation. Validation observes raw and calculated tables; no business metric reads a PASS/FAIL diagnostic cell.

## Formulas and missing-data rules

Use Excel-invariant formulas and bounded ranges/tables. Final exporter should extend the table and formula ranges to the validated row count, with a clear export boundary; do not promise unbounded refresh. Examples below show concepts, not exact cell positions in every export.

| Result | Formula/rule |
|---|---|
| Duration | IF either endpoint is blank or clock domains differ, unavailable; otherwise end_ms - start_ms. Negative result is an error, not clamped to zero. |
| Eligible adjudicated claims | COUNTIFS(truth,"supported",eligible,TRUE) + COUNTIFS(truth,"contradicted",eligible,TRUE) |
| Contradicted rate | IF(n=0,"Unavailable",contradicted/n), with x and n in separate numeric cells |
| Coverage | IF(eligible_extracted=0,"Unavailable",adjudicated/eligible_extracted) |
| Recovery rate | verified / eligible_observed_failure_runs; unknown/failed/censored counts displayed separately |
| Extra effects | If observer complete: MAX(0,observed_cardinality - allowed_cardinality); otherwise unavailable |
| Cost | If all required categories/prices known: SUMPRODUCT(disjoint_units,unit_prices) + fees. Otherwise show known subtotal and unknown request count, with completeness partial. |
| Paired delta | candidate - matched baseline, only with matching_status valid and both values known |
| Wilson interval | p=x/n; center=(p+z²/(2n))/(1+z²/n); half=z*SQRT(p*(1-p)/n+z²/(4n²))/(1+z²/n). Bounds clipped to [0,1]. Use only with stated independent-binomial assumptions. |

Never use IFERROR(...,0) to turn missing evidence into success. Guard zero denominators explicitly. Reasoning tokens already included in output do not add a second charge. Blank cells and explicit zeros differ. A no-fault run has recovery not_applicable, not recovered. Scorer agreement, extraction coverage and truth accuracy have distinct denominators. Live/simulation/synthetic rows never share a rate.

## Example workbook contract

The sample is deliberately small: six synthetic app-family runs (three policies, clean versus post-commit crash), a selected-run timeline, attempts, effect observations, recovery episodes, exact claims, evidence and illustrative usage. It demonstrates workbook structure only. It does not demonstrate implemented support for app generation, homework or math; those belong to the application plan. All six runs use synthetic values and no actual model name/provider billing.

Policy comparisons are linked to run rows. Timeline detail covers only the selected reconciled run and is labeled as such; it is not a complete trace for every sample run. All displayed claim/effect/call judgments resolve to synthetic evidence records. No synthetic precision is presented as a measured reliability result. Price inputs are arbitrary example rates labeled synthetic, not current provider prices. Confidence intervals are omitted from the tiny invented sample.

## Export and validation acceptance

1. Validate schema, uniqueness, enum/type/unit rules, foreign keys, complete raw sidecar hashes and metric inclusion before building.
2. Reconcile rows/IDs against the JSON manifest; compare run totals, physical attempts, effect counts, extracted/adjudicated claims, known cost and unknown requests independently.
3. Recalculate formulas, scan error cells and trace each headline to source inputs. Test blank versus zero, a missing denominator, a failed/unknown observer, missing usage and a changed source outcome in a disposable state, then restore inputs.
4. Render every sheet, inspect headers/columns and fix clipped/ambiguous content. Verify chart series point to calculated ranges. Render wide sheets in readable panels; do not shrink text to make 30 fields fit one screen.
5. Export XLSX, inspect its stored formulas/cached values and expected sheet/table/chart counts. Native Excel interactive behavior remains unverified until opened in Excel; report that limitation.
6. Export a manifest containing workbook digest, raw evidence digest and counts, schema/export version, mode and selection. Signed provenance, if generated, proves integrity/self-declared tool attribution only, not benchmark accuracy.
