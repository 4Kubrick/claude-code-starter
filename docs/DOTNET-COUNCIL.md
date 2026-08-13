# .NET + Ask the Council extension

This fork keeps the original Claude Code Starter workflow and adds a focused .NET specialization layer.

## Added stack coverage
- modern .NET / C# / ASP.NET Core
- EF Core
- .NET MAUI
- WinForms + DevExpress
- SQL Server / PostgreSQL / SQLite
- SignalR / RabbitMQ / Quartz.NET
- Docker / NGINX
- Grafana / Loki

## Ask the Council

Use `/ask-council` for consequential decisions that benefit from several independent perspectives.

Examples:

```text
/ask-council
Should this .NET SaaS use SQL Server or PostgreSQL?
```

```text
/ask-council
Review replacing polling with SignalR in this MAUI application.
Consider battery usage, reconnect behavior, backend complexity and observability.
```

```text
/ask-council
Should this MVP ship loyalty stamps, points, or both?
Consider user value, implementation cost and pilot learning speed.
```

The council intentionally reuses generic upstream agents (for example performance, simplicity and research reviewers) and adds stack-specific agents only where specialization materially improves the review.

## Recommended panels

### .NET architecture
- council-chair
- dotnet-architect
- dotnet-backend
- database-architect-dotnet
- security-dotnet
- performance-oracle
- devils-advocate

### MAUI performance / architecture
- council-chair
- maui-engineer
- dotnet-backend
- performance-oracle
- code-simplicity-reviewer
- devils-advocate

### WinForms / DevExpress upgrade
- council-chair
- winforms-devexpress
- dotnet-architect
- framework-docs-researcher
- code-simplicity-reviewer
- devils-advocate

### Product / MVP
- council-chair
- product-manager
- customer-advocate
- startup-gtm
- devils-advocate

## Design rule

Do not run the council for routine coding tasks. The upstream workflow remains the default. Council is an escalation mechanism for decisions with meaningful trade-offs, uncertainty, or cost of reversal.