# Claude Code .NET Starter

.NET-first fork of Claude Code Starter.

## Supported stack

- C# / modern .NET
- ASP.NET Core
- Entity Framework Core
- SQL Server, PostgreSQL and SQLite
- .NET MAUI
- WinForms + DevExpress
- Blazor
- SignalR, RabbitMQ and Quartz.NET
- Docker / NGINX / CI/CD
- structured logging and observability

## What stays from upstream

The generic workflow remains useful for brainstorming, planning, repository research, documentation, code review, security, performance, simplicity analysis, browser tooling and knowledge capture.

## What changed

The fork is no longer tuned primarily for React + TypeScript + Supabase + Vite + Tailwind. `.NET` routing is authoritative whenever the repository contains a .NET solution/project. Legacy frontend-specific assets are not selected for .NET work.

## .NET specialists

- `dotnet-architect`
- `dotnet-backend`
- `database-architect-dotnet`
- `maui-engineer`
- `winforms-devexpress`
- `security-dotnet`
- `devops-dotnet`

Generic reviewers such as `performance-oracle`, `code-simplicity-reviewer`, `security-sentinel`, `architecture-strategist` and research agents remain available.

## Ask the Council

Use `/ask-council` for consequential architecture, migration, security, performance, production or product decisions. Council members analyze independently, challenge assumptions and `council-chair` synthesizes the recommendation.

Example:

```text
/ask-council
Should this MAUI application replace REST polling with SignalR?
Consider reconnect behavior, battery usage, backend complexity and testability.
```

## Normal workflow

Use the upstream planning flow, but follow `.claude/rules/dotnet-stack.md` for implementation and validation. Inspect `.sln`/`.slnx`, `.csproj`, `Directory.Build.*`, package management, configuration, migrations and tests before choosing tools or architecture.

Typical validation is `dotnet restore` when needed, then `dotnet build`, then targeted tests before broader suites. For MAUI/WinForms, distinguish automated validation from device/manual UI validation.

See `CLAUDE.md` and `docs/DOTNET-COUNCIL.md` for the .NET routing and council behavior.
