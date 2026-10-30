# From findings to better code

## Define the permitted action

Record the project's existing authority and constraints in its operating contract. Review-only produces findings. Prepare mode produces a reviewable local change or authorized PR. Implement mode may make bounded changes within the authorized scope. Release follows the project's actual release policy, not an inference from this skill.

Persist the scope: repositories/branches, permitted change classes, test commands, maximum work per run, release authority and stop/escalation conditions. Analysis credentials should be read-only where possible; a reviewer does not need production write access. Isolate coding from raw untrusted log content and use sanitized evidence packets.

## One measured change

Select the highest-impact actionable finding that fits the permitted scope. If evidence is insufficient, improve measurement or run a targeted diagnostic first. Record the finding ID, baseline, hypothesis, expected benefit, regression guardrails and a practical rollback before editing.

Reproduce the failure where possible, then implement the smallest useful fix in an isolated branch/worktree or the project's established workflow. Add a regression check for a concrete failure when appropriate; test the actual visible outcome and persistence/external result, not only the function that emits a success event. Run checks proportionate to the changed behavior and existing requirements.

Review the final diff for unrelated changes, privacy/telemetry expansion and instrumentation changes that could fake an improvement. Do not change the success metric or suppress error events to make the app appear healthier. Capture the exact change, checks and release identifier. Follow existing production-change rules for deployment, migration and rollback.

## Close the loop after release

Compare matched journeys, versions and eligible populations before and after the change. Prefer a controlled comparison where available. Otherwise report a before/after association with plausible confounders: traffic mix, workload, provider incidents, releases and telemetry changes. Report numerator, denominator, observation window and uncertainty.

Use one primary outcome such as successful task completion and a few guardrails such as tail latency, cost, error rate and privacy. Choose a minimum evidence window/sample appropriate to the app; sparse usage stays pending rather than becoming a claim of success. Aggregate evidence can miss a severe individual regression, so keep incident inspection.

Maintain a ledger with finding ID, baseline, change reference, tested result, release/version, observation window, measured result, decision and follow-up. Statuses can be proposed, prepared, released-awaiting-evidence, improved, inconclusive, regressed or rolled-back. Do not call an unreleased or unmeasured change improved.

Re-rank the backlog each day using new evidence. Avoid fixing the same cause repeatedly, oscillating between contradictory changes, or stacking unmeasured changes that obscure attribution. No meaningful traffic or no supported improvement means a no-change decision, not forced code churn.
