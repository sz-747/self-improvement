# Instrumentation and experience reconstruction

## Plan from the journey

Create an event map with columns: user goal, action, visible states, internal stages, persistence/external effects, expected outcome, failure/timeout/cancellation signals, correlation fields, allowed data, and verification method. Cover background work, retries, crashes, offline operation and app restarts when applicable.

For example, a save journey needs `save_requested`, validation and persistence evidence, and `save_result_displayed`. Link them with an operation ID. A successful backend write followed by a stuck spinner is a different finding from a failed write. A displayed success followed by data loss is another. Confirm actual persistence through an appropriate check rather than inferring it from a log message.

## Event contract

Use the existing structured logging format. Define equivalent fields where names differ:

| Fields | Purpose |
|---|---|
| `event_id`, `schema_version`, `event_name` | Unique deduplication key and stable interpretation |
| `occurred_at`, `ingested_at` | UTC event and arrival times; preserve original precision |
| `service`, `environment`, `app_version`, `release_id` | Identify the executable and deployment |
| `session_id`, `operation_id`, `trace_id`, `span_id`, `parent_span_id` | Join user intent to internal and background stages as applicable |
| `sequence`, monotonic duration, clock quality | Order events within a producer despite clock skew |
| `journey`, `stage`, `status`, `reason_code` | Machine-readable behavior; distinguish pending from terminal states |
| `visible_state`, `outcome`, `outcome_check` | What the user saw and how success was checked |
| `duration_ms`, retry/attempt count, queue delay, resource/cost units | Locate wasted time and work |
| allowlisted dimensions and restricted artifact references | Useful context without unrestricted payload capture |

Record asynchronous links across queues and process restarts. Define terminal expectations and timeout rules so a missing completion event can be detected. Cancellation is not automatically a failure. Deduplicate retries without hiding repeated attempts or repeated side effects.

For AI stages, record configured provider/model identifier, prompt/template version, permitted input/output summaries or references, tool calls and outcomes, latency, usage, validation and user corrections. Do not require hidden chain-of-thought or assume model output is correct because generation completed.

For command-line, desktop, service and browser software, choose equivalent outcome signals. DOM snapshots are optional and browser-specific, not a universal prerequisite.

## Reconstruction versus replay

- **Timeline reconstruction:** ordered, correlated actions, internal stages and observed outcomes. Explicitly mark unknown state, clock ambiguity and missing spans.
- **Visual replay:** separately authorized screenshots or masked UI captures with meaningful timestamps. Capture only allowed surfaces; a stream of click names cannot recreate pixels.
- **Execution replay:** a controlled environment with compatible build/configuration, permitted input/state snapshots, recorded external responses or stubs, and nondeterminism accounted for. Disable real external side effects and use disposable data. Never replay a payment, message or destructive action against production.

Retain replay references only while their artifacts remain available. Report expired/deleted/redacted artifacts as unavailable; do not fabricate their contents. Explain how redaction limits fidelity.

## Collection boundaries and health

Define event allowlists, masking at capture, access controls, retention/deletion, encryption where appropriate and per-device/session linkage policy. Exclude credentials, tokens, keystroke streams, unrestricted request/response bodies and user documents by default. Raw content or visual captures require a specific diagnostic need and permitted handling. An aggregate-only consent choice must not silently enable raw session recording.

Set queue/storage bounds, rotation, upload policy, rate limits and measurable overhead budgets. Expose dropped events, sample rates, export lag, schema failures and disabled collection. Prefer full lightweight critical-journey events and bounded detail; if sampling occurs, carry the policy into every analysis.

Test: normal success, a failure, interruption/missing terminal event, and collector/storage failure. Inspect emitted data for secrets and personal content using synthetic fixtures. Confirm logging failure does not block the user's main action and that loss is visible to the reviewer. Keep diagnostic delivery separate from security audit requirements if the project already has them.
