# Claude Code .NET Starter

This fork is .NET-first. Preserve the upstream planning/research/documentation workflow, but choose .NET specialists and .NET validation commands by default.

## Default stack

Assume modern C# and .NET unless the repository proves otherwise. Detect the actual target framework from project files before proposing upgrades.

Primary technologies supported:
- C# / .NET 8-10
- ASP.NET Core Web API and Minimal APIs
- Entity Framework Core
- SQL Server, PostgreSQL and SQLite
- .NET MAUI
- WinForms and DevExpress
- Blazor
- SignalR, RabbitMQ and Quartz.NET
- Docker, NGINX and standard CI/CD
- structured logging and OpenTelemetry-compatible observability

## Repository-first behavior

Before implementation, inspect `.sln`/`.slnx`, `.csproj`, `Directory.Build.*`, `Directory.Packages.props`, `global.json`, `appsettings*.json`, migration folders, tests and existing conventions. Do not impose a template architecture on an established codebase.

## Agent routing

Prefer these specialists for stack-specific work:
- `dotnet-architect` — architecture and boundaries
- `dotnet-backend` — ASP.NET Core, services, APIs, async/concurrency
- `database-architect-dotnet` — EF Core, SQL Server/PostgreSQL/SQLite
- `maui-engineer` — .NET MAUI
- `winforms-devexpress` — WinForms and DevExpress
- `blazor-engineer` — Blazor UI and hosting models
- `security-dotnet` — authentication, authorization and OWASP for .NET
- `devops-dotnet` — Docker, hosting, CI/CD and observability
- `dotnet-test-reviewer` — unit/integration/UI testing and test quality

Generic upstream specialists such as `performance-oracle`, `architecture-strategist`, `security-sentinel`, `code-simplicity-reviewer`, `repo-research-analyst` and research agents remain useful when their scope is technology-independent.

Do not select `kieran-typescript-reviewer`, React/Tailwind or Supabase guidance for a .NET repository unless the repository actually contains that stack.

## Council

Use `/ask-council` for consequential architecture, migration, security, performance, product or technology decisions. Council members should analyze independently before the chair synthesizes the answer. Include `devils-advocate` for expensive-to-reverse choices.

## Validation

For .NET changes, use the narrowest relevant commands and expand only as needed:
1. `dotnet restore` when dependencies/assets changed or are missing.
2. `dotnet build --no-restore` for compile validation.
3. `dotnet test --no-build` after a successful build when practical.
4. Run targeted test projects/filters before the whole solution on large repositories.
5. For EF Core schema changes, inspect generated migrations and SQL implications.
6. For MAUI/WinForms, distinguish compile validation from platform/device/manual UI validation.

Never weaken tests merely to make the pipeline green. Do not change public contracts, database schemas or authentication behavior without calling out compatibility impact.
