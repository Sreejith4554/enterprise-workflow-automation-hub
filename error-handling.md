# Error Handling & Observability

## Failure classes

1. **Validation failure** — missing required business fields. Route to manual correction; do not retry automatically.
2. **Transient connector failure** — rate limit, timeout or temporary 5xx. Retry with bounded exponential backoff.
3. **Authorization failure** — expired/invalid credential. Stop retries quickly and alert the workflow owner.
4. **Downstream business rule failure** — invalid Jira project/component or removed owner. Send to a dead-letter queue with context.

## Idempotency

Use `source:external_id` as a correlation key. Before creating a Jira issue, check the tracker for an existing key. If present, update the existing record or exit safely.

## Minimum operational metrics

- executions / day
- success rate
- median processing time
- retry count
- dead-letter count
- duplicate-prevention count
- SLA escalation count

## Recovery

A failed item should be replayable after correction without creating duplicate tickets. Log enough metadata to reproduce the original request while avoiding sensitive message content where not required.
