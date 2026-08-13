# .NET Stack Routing

When the repository contains `.sln`, `.csproj`, C# or XAML, this file is authoritative for stack-specific routing and validation. Keep the generic upstream pipeline, planning, review and knowledge-base mechanisms, but do not force React/Supabase/Vite commands or conventions onto .NET projects.

## Agent routing
- Architecture / solution boundaries -> `dotnet-architect`
- ASP.NET Core, C#, Web API, EF Core, SignalR, RabbitMQ, Quartz.NET -> `dotnet-backend`
- .NET MAUI Android/iOS -> `maui-engineer`
- WinForms / DevExpress -> `winforms-devexpress`
- SQL Server / PostgreSQL / SQLite / EF Core persistence -> `database-architect-dotnet`
- Security -> `security-dotnet`
- Docker / NGINX / CI/CD / Grafana / Loki -> `devops-dotnet`

The existing orchestration agents keep their names for workflow compatibility:
- `feature-builder-data` = .NET backend/data builder
- `feature-builder-ui` = MAUI/WinForms/DevExpress/Blazor UI builder
- `feature-builder-fullstack` = .NET cross-layer builder
- `feature-tester-e2e` = stack-aware browser/native smoke tester

Reuse upstream agents for generic performance, simplicity, repo research and documentation research.

## Project detection before work
Inspect, in order:
1. `.sln` / `.slnx`
2. `.csproj` and `TargetFramework*`
3. `Directory.Build.props` / `Directory.Packages.props`
4. test projects and CI files
5. `appsettings*` / launch profiles
6. package manifests only if the solution actually has a separate JS frontend

Do not infer the stack only from this starter repository.

## Validation policy
For .NET-only repositories, the default gate is:
1. restore only when necessary
2. `dotnet build` using the solution/project and configuration used by the repo
3. relevant `dotnet test`
4. configured analyzers/formatter if present
5. platform-specific build/smoke when the change needs it

Never fail a .NET IU because `tsc`, `vitest`, `eslint`, `vite build`, Supabase CLI or Tailwind tooling is absent. Those checks apply only to an actual JS frontend in the target repository.

For mixed .NET + JS solutions, validate each changed side with its own toolchain.

## UI verification
- Blazor/web: browser E2E is appropriate when a runnable HTTP UI exists.
- MAUI: prefer platform build + existing automation + explicit manual smoke when no native harness exists.
- WinForms/DevExpress: build/test + existing UI automation or explicit manual smoke; browser tools are not a substitute.

## Council policy
Use `ask-council` when the choice is expensive to reverse, several disciplines conflict, a production incident has multiple plausible causes, or the user explicitly wants independent perspectives. Keep panels to 3-7 agents and include `devils-advocate` for high-impact choices.

## Engineering defaults
- Prefer incremental changes over rewrites.
- Preserve existing conventions unless they cause a concrete problem.
- Use async/cancellation correctly.
- Treat observability and rollback as part of production design.
- Measure performance before optimizing.
- For DevExpress/.NET upgrades, verify removed/obsolete APIs and version-specific behavior before changing code.
- Do not introduce Clean Architecture, DDD, CQRS, MediatR or microservices merely because they are common .NET patterns; require a concrete benefit in the target project.
