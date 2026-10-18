# Upstream schedules paused in this fork

Paused 29 scheduled agentic workflows (gh-aw compiled `.lock.yml`) by adding a gate to each root job:

```yaml
if: github.event_name != 'schedule' || vars.ENABLE_UPSTREAM_SCHEDULES == 'true'
```

Nothing was deleted. `workflow_dispatch` and other triggers still run.

## Resume
- All at once: Settings → Secrets and variables → Actions → Variables → add `ENABLE_UPSTREAM_SCHEDULES` = `true`.
- Per workflow: remove the gate line (or the `(gate) && (...)` wrapper) from that lock file, or recompile from its `.md` with `gh aw compile`.

## Why
These are the upstream github/gh-aw-mcpg fleet. In this fork they fail in setup because upstream secrets/config are absent, producing hundreds of failure emails a day.

## Secrets they reference (add before resuming)
Token secrets (the `github-token` inputs): `GH_AW_GITHUB_TOKEN`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `CROSS_REPO_PAT`, `GH_AW_MCP_MULTIREPO_TOKEN`.

| Secret | Workflows referencing it |
|---|---|
| `GH_AW_GITHUB_MCP_SERVER_TOKEN` | 29 |
| `GH_AW_GITHUB_TOKEN` | 29 |
| `GH_AW_DEFAULT_OTLP_HEADERS` | 28 |
| `GH_AW_CI_TRIGGER_TOKEN` | 7 |
| `CROSS_REPO_PAT` | 1 |
| `GH_AW_MCP_MULTIREPO_TOKEN` | 1 |
| `GH_AW_OTEL_SENTRY_AUTHORIZATION` | 1 |
| `GH_AW_OTEL_SENTRY_ENDPOINT` | 1 |

## Per-workflow secrets

- `daily-compliance-checker.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `duplicate-code-detector.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `gateway-issue-dispatcher.lock.yml`: `CROSS_REPO_PAT`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `ghcr-download-tracker.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `github-mcp-guard-coverage-checker.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `go-fan.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `go-logger.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `gpl-dependency-checker.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `guard-status-tracker.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `integrity-filtering-audit.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `large-payload-tester.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `mcp-gateway-log-analyzer.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`, `GH_AW_MCP_MULTIREPO_TOKEN`
- `nightly-docs-reconciler.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `nightly-schema-updater.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `nightly-workflow-compiler.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `repo-assist.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `rust-guard-improver.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `semantic-function-refactor.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-allowonly.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-copilot.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-long-session.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-otel-tracing.lock.yml`: `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`, `GH_AW_OTEL_SENTRY_AUTHORIZATION`, `GH_AW_OTEL_SENTRY_ENDPOINT`
- `smoke-safeoutputs-discussions.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-safeoutputs-issues.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-safeoutputs-labels.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-safeoutputs-prs.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `smoke-safeoutputs-reviews.lock.yml`: `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `test-coverage-improver.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
- `test-improver.lock.yml`: `GH_AW_CI_TRIGGER_TOKEN`, `GH_AW_DEFAULT_OTLP_HEADERS`, `GH_AW_GITHUB_MCP_SERVER_TOKEN`, `GH_AW_GITHUB_TOKEN`
