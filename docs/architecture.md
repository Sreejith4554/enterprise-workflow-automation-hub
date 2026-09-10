# Architecture

## Components

| Component | Responsibility | Control |
|---|---|---|
| Intake channel | Capture new risk/issue/action/blocker | Required fields + external ID |
| Orchestrator | Validate, normalize and route | Schema validation + correlation ID |
| Jira | Delivery execution record | Issue key + workflow state |
| SharePoint-style tracker | Portfolio-level RAID/OPL view | Unique idempotency key |
| Teams/Slack notification | Owner awareness | Severity/SLA threshold |
| Audit log | Trace execution and failures | Immutable correlation data |

## Data contract

The workflow treats `external_id + source` as the idempotency key. A repeated message should update or no-op rather than create another ticket.

## Ownership model

- **Workflow owner:** accountable for automation reliability and change control.
- **Process owner:** defines business rules and severity/SLA thresholds.
- **Workstream owner:** owns the underlying action or blocker.
- **PMO/operations coordinator:** reviews dead-letter items and systemic exceptions.

## Integration note

All URLs and credentials in this portfolio are placeholders. In production, use approved connectors, a secrets store, least-privilege service accounts and environment-specific configuration.
