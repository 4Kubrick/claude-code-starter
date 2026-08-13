# .NET Stack Routing

When the repository contains .NET/C# projects, prefer the .NET-specific agents for stack-specific questions while keeping the upstream workflow/pipeline intact.

## Agent routing
- Architecture and solution boundaries -> `dotnet-architect`
- ASP.NET Core, C#, EF Core, SignalR, RabbitMQ, Quartz.NET -> `dotnet-backend`
- .NET MAUI Android/iOS -> `maui-engineer`
- WinForms / DevExpress -> `winforms-devexpress`
- SQL Server / PostgreSQL / SQLite / EF Core persistence -> `database-architect-dotnet`
- Security -> `security-dotnet`
- Docker / NGINX / CI/CD / Grafana / Loki -> `devops-dotnet`

Reuse upstream agents for generic concerns such as performance, simplicity, repository research, documentation research and broad architecture review.

## Council policy
Use `ask-council` when:
- the choice is expensive to reverse,
- several disciplines are involved,
- architecture/security/performance trade-offs conflict,
- a production incident has multiple plausible root causes,
- the user explicitly asks for several expert perspectives.

Do not use a council for trivial coding tasks. Keep panels to 3-7 agents.

## Engineering defaults
- Prefer incremental changes over rewrites.
- Preserve existing conventions unless they cause a concrete problem.
- Use async/cancellation correctly.
- Treat observability and rollback as part of production design.
- Measure performance before optimizing.
- For upgrades (especially DevExpress/.NET), verify removed/obsolete APIs and migration behavior before changing code.