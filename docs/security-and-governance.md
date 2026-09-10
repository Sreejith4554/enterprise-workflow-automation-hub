# Security & Governance

- Never commit credentials, API tokens or production tenant URLs.
- Use environment variables / credential stores and rotate secrets.
- Grant service accounts only the permissions required for the workflow.
- Avoid logging unnecessary personal or message-body data.
- Separate development, test and production environments.
- Version workflow exports and document rule changes.
- Define a change owner for severity mappings, SLA thresholds and field schemas.
- Include a manual fallback when automation cannot safely determine ownership.
