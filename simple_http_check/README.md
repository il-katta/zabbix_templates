# Simple HTTP Check

Zabbix template for monitoring HTTP service availability and performance.

Template file: [Simple HTTP check.yaml](Simple%20HTTP20check.yaml)


## Requirements

No installation required. The Zabbix server or proxy must be able to reach the target host on the configured HTTP port.

## Macro Configuration

### Optional macros

- **{$HTTP_PORT}**: HTTP port to check (default: `80`)

## What it monitors

This template monitors:
- **HTTP Service availability**: Checks if the HTTP service is responding
- **HTTP Performance**: Measures the response time in seconds

## Triggers

- **HTTP Service down**: Triggered with HIGH priority when the HTTP service is not responding
