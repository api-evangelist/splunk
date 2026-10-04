---
name: splunk-create-monitor-input
description: Create a new file or directory monitor input and retrieve its details.
api: openapi/splunk-data-inputs-api-openapi.yml
operations:
- createMonitorInput
- getMonitorInput
generated: '2026-10-03'
method: generated
generator: extract-docs-artifacts.py skills (local)
source: openapi/splunk-data-inputs-api-openapi.yml ; every operationId checked against the contract
---

# splunk-create-monitor-input

Create a new file or directory monitor input and retrieve its details.

## Steps

1. 1. Call `createMonitorInput` with required body fields (e.g., `name`, `index`, `sourcetype`).
2. 2. Call `getMonitorInput` with the `name` path parameter to verify the input was created.

## Rules

- Auth: Include a valid Bearer token in the `Authorization` header (or use BasicAuth or HecToken as supported).
- Idempotency: `createMonitorInput` is not idempotent; repeat calls will create duplicate inputs unless the same `name` is used.
