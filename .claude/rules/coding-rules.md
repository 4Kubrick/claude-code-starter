# Coding Rules — .NET-first

These rules are the default when the repository contains `.sln`, `.csproj`, C# or XAML. If a project intentionally uses another stack, follow the repository's own conventions instead of forcing .NET rules onto it.

## 1. Scope and simplicity

- Prefer the smallest change that solves the requested problem.
- Do not refactor unrelated code while implementing a feature or fix.
- One class/module should have one clear responsibility.
- Extract an abstraction only when it removes real duplication or clarifies a stable boundary.
- Prefer incremental modernization over rewrites, especially in WinForms/DevExpress codebases.
- Preserve public contracts unless changing them is explicitly part of the task.

## 2. C# conventions

- Use modern C# supported by the target framework; inspect `TargetFramework`/`LangVersion` first.
- Public types/members: `PascalCase`; locals/parameters/private fields: normal .NET conventions (`camelCase`, `_field`).
- Interfaces use the normal .NET `I` prefix when the codebase does so.
- Prefer nullable reference types and explicit null handling over `!` suppression.
- Prefer records/value objects only where value semantics are useful; do not convert classes mechanically.
- Prefer `var` when the type is obvious from the right-hand side; otherwise favor readability.
- Do not introduce clever LINQ when a simple loop is clearer or materially faster.

## 3. Async, cancellation and resources

- Never block async code with `.Result`, `.Wait()` or `.GetAwaiter().GetResult()` in application paths unless a framework boundary genuinely requires it.
- Propagate `CancellationToken` through I/O, EF Core, HTTP, SignalR and background operations when cancellation is meaningful.
- Use `await using`/`using` for disposable resources.
- Do not use `async void` except event handlers.
- Avoid fire-and-forget tasks unless ownership, exception handling and lifetime are explicit.
- Treat UI thread affinity explicitly in MAUI/WinForms; expensive work must not run on the UI thread.

## 4. Error handling and logging

- Never swallow exceptions with empty `catch` blocks.
- Catch specific exceptions when recovery is possible; otherwise let the failure propagate to the appropriate boundary.
- Use structured logging through the project's logging stack (`ILogger`, NLog, Serilog, etc.); no production `Console.WriteLine` debugging.
- Do not log secrets, access tokens, connection strings or unnecessary PII.
- ASP.NET Core APIs should return consistent problem/error responses; prefer framework `ProblemDetails` when it fits the project.
- Do not use exceptions for normal control flow.

## 5. ASP.NET Core / APIs

- Validate input at the API boundary.
- Authentication and authorization are separate concerns; enforce authorization server-side.
- Never trust roles/claims sent by a client without server verification.
- Use DI with correct lifetimes; do not capture scoped services in singletons.
- Prefer typed options/configuration over scattered environment-variable reads.
- Public endpoints should consider rate limits, idempotency and abuse cases where relevant.
- Preserve backwards compatibility of external API contracts unless a breaking change is intentional.

## 6. EF Core and databases

- Avoid N+1 queries. Inspect generated query shape when Includes/navigation access are involved.
- Prefer projections (`Select`) for read models instead of materializing full entities when only a subset is needed.
- Use `AsNoTracking()` for read-only queries when appropriate.
- Do not call `ToList()`/`AsEnumerable()` early and accidentally move filtering to memory.
- Use parameterized SQL; never concatenate user input into SQL.
- Migrations must be reviewable and safe for existing data. Consider rollback/forward-fix strategy.
- Keep transactions as short as practical and understand isolation/concurrency implications.
- For SQL Server/PostgreSQL/SQLite differences, do not assume provider behavior is identical.

## 7. MAUI

- Keep the UI thread responsive; measure navigation/startup/list rendering before optimizing.
- Respect Android/iOS lifecycle and permission differences.
- Dispose/unsubscribe long-lived handlers, timers and events that can retain pages/view-models.
- For `CollectionView`, avoid expensive bindings/converters and unnecessary full collection replacement.
- Use local SQLite/offline synchronization deliberately; define conflict/retry behavior instead of hiding failures.
- Sensitive local data belongs in secure storage where appropriate, not plain preferences/logs.

## 8. WinForms / DevExpress

- Preserve event lifecycle and UI-thread rules.
- Long-running operations should not block the message loop.
- Dispose controls/components/resources correctly.
- When upgrading DevExpress, verify obsolete/removed APIs and behavioral changes before replacing code.
- Prefer focused compatibility fixes over broad redesign of stable legacy forms.
- Treat designer-generated files carefully; do not hand-edit generated code unless the framework workflow requires it.

## 9. Testing

- Never weaken or delete a valid test merely to make the suite green.
- Test behavior, not implementation details.
- New business logic should normally include happy-path and failure/edge coverage.
- Use the project's existing framework (`xUnit`, `NUnit`, `MSTest`, UI/integration tooling) rather than introducing another one casually.
- For ASP.NET Core integration tests, prefer realistic application boundaries when authorization/data behavior matters.
- For EF Core, do not use an in-memory provider when provider-specific SQL behavior is what needs verification.
- Do not claim completion before relevant tests/build pass or before clearly reporting why they cannot run.

## 10. Validation commands

Discover the solution/project first. Typical .NET gate:

1. `dotnet restore` only when required
2. `dotnet build --no-restore` (or the repository's build script)
3. `dotnet test --no-build` for the relevant solution/projects
4. formatter/analyzers if the repository configures them (`dotnet format`, Roslyn analyzers, StyleCop, etc.)
5. platform-specific build when relevant (MAUI Android/iOS, WinForms target framework)

Do not blindly run Node/Vite/Vitest commands in a .NET-only repository. If the solution contains a web frontend too, validate that frontend separately using its own package scripts.

## 11. Dependencies

- Inspect `.csproj`, `Directory.Packages.props`, `packages.lock.json` and NuGet configuration before adding packages.
- Prefer existing dependencies and BCL/framework capabilities over a new package.
- Do not upgrade unrelated packages during a feature/fix.
- For a new NuGet package, check maintenance, licensing, target-framework compatibility and operational impact.

## 12. Security

- Never commit secrets, API keys, certificates, tokens or production connection strings.
- Never build SQL from concatenated user input.
- Validate file uploads, paths and external URLs; consider traversal/SSRF risks.
- Protect state-changing web endpoints against the relevant auth/CSRF threat model.
- Store MAUI secrets using platform-secure facilities when possible.
- Treat deserialization of untrusted input as a security boundary.
- Apply least privilege to database/service credentials.

## 13. Performance

- Measure before optimizing.
- Flag O(n²) work on potentially large collections.
- Avoid repeated database/network calls inside loops; batch when possible.
- Watch allocations in hot paths and UI list rendering, but do not micro-optimize ordinary code.
- For MAUI/WinForms performance issues, distinguish UI-thread work, data access, rendering/binding and network latency.

## 14. Architecture

- Keep dependency direction explicit. UI should not talk directly to persistence unless the existing application is intentionally structured that way.
- Avoid circular project references.
- Prefer modular monolith boundaries before introducing distributed-system complexity without a concrete need.
- Background jobs, messaging (RabbitMQ), SignalR and schedulers (Quartz.NET) require explicit retry/idempotency/failure handling.
- Production changes should be observable and have a rollback or recovery strategy.

## 15. AI-specific guardrails

- Inspect the repository before assuming framework/version/package availability.
- Do not invent APIs from memory when a library/version can be checked locally.
- Do not alter tests, analyzers or quality thresholds to hide a defect.
- Do not dismiss review findings as “pre-existing” without reporting them.
- Do not create speculative layers/configuration for scenarios outside the task.
- If an instruction is ambiguous but the answer can be discovered from code/config, discover it instead of asking.
