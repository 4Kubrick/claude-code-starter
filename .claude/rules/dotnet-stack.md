# .NET Stack Routing

When the repository contains `.sln`, `.slnx`, `.csproj` or C# source, this rule is authoritative for stack-specific work.

## Prefer
- Architecture -> `dotnet-architect`
- ASP.NET Core / C# / APIs / SignalR / RabbitMQ / Quartz.NET -> `dotnet-backend`
- .NET MAUI -> `maui-engineer`
- WinForms / DevExpress -> `winforms-devexpress`
- SQL Server / PostgreSQL / SQLite / EF Core -> `database-architect-dotnet`
- Security -> `security-dotnet`
- Docker / NGINX / CI/CD / observability -> `devops-dotnet`

Reuse generic upstream agents for repository research, performance, simplicity, security review and documentation research.

## Do not route .NET work to
- `kieran-typescript-reviewer`
- `feature-builder-ui`
- `feature-builder-fullstack`
- `feature-builder-data`
- `tailwind-react-guidelines`
- `supabase-dev-guidelines`

unless the inspected repository actually contains those technologies.

## Validation defaults
1. Detect target framework and solution/project structure.
2. Restore only when dependency assets require it.
3. Build the narrowest relevant project/solution.
4. Run targeted tests before broader suites.
5. Treat MAUI/WinForms compile validation separately from device/manual UI validation.
6. Inspect EF Core migrations and provider differences for schema changes.

## Council policy
Use `ask-council` for expensive-to-reverse choices, architecture/security/performance trade-offs, migrations, production incidents with competing hypotheses, or explicit multi-expert requests. Keep panels focused.