# Optional population analysis

Start with the project's permitted telemetry scope, collection notice/consent controls where applicable, retention and allowed analysis destinations. This skill does not establish legal compliance or authorize transferring raw logs to an external model. Prefer local/on-device aggregation or sanitized summaries when they answer the question.

Define the unit for every metric: event, operation, session, installation or person. Do not call installations unique people. Use only necessary pseudonymous linkage, keep identity mappings separate when needed, and treat pseudonymous records as sensitive. Avoid collecting names, full URLs/query strings, document text or unrestricted device fingerprints for convenience.

Build metrics around outcomes: completion funnels, failures and recovery, latency distributions, retries, corrections, repeated work, resource/cost per completed task, and recurring friction. Define eligible population and denominators. Segment by journey, app version, platform and meaningful workload where justified. Suppress small groups under a project-defined threshold and omit identifying dimensions from reports; suppression alone is not a guarantee of anonymity.

Carry collection coverage, sampling method/probability, opt-outs, missing terminal events, duplicates, export delays and version/schema changes into the analysis. A drop in errors can mean collection stopped. Opt-in users may differ from everyone else. Prefer rates and distributions over raw totals when traffic changes; averages can hide slow or broken tails.

Keep population-wide patterns and severe individual failures visible together. A single-user local app can aggregate across sessions, but must not claim multi-user demand or generalize to a population it did not observe.

For each proposed improvement, show observed association, affected population, uncertainty and the test needed to establish benefit. Use controlled experiments when justified and authorized; otherwise label observational comparisons. Do not infer user motivation, satisfaction or causation from click frequency alone.

Verify filtering/opt-out, redaction, access, expiry/deletion and aggregate accuracy with synthetic records before activation. Confirm deletion behavior across raw events, derived records, backups and replay artifacts according to the project's retention contract. Document residual limitations instead of promising universal erasure or anonymity.
