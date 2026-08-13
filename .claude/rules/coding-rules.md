# Coding Rules — .NET first

These rules are the default when the repository contains `.sln`, `.slnx`, `.csproj`, C# or XAML. Always prefer the target repository's established conventions over generic starter assumptions.

## Scope
- Make the smallest change that solves the requested problem.
- Do not refactor unrelated code.
- Preserve public contracts unless the task explicitly changes them.
- Prefer incremental modernization over rewrites, especially in WinForms/DevExpress.

## C# and async
- Inspect target framework and language version before using newer features.
- Follow nullable reference type conventions used by the project.
- Avoid sync-over-async in application code.
- Pass `CancellationToken` through meaningful I/O paths.
- Dispose resources deterministically.
- Avoid `async void` except UI/event handlers.

## ASP.NET Core
- Validate at system boundaries.
- Keep dependency injection lifetimes correct.
- Use the project's established error response and logging conventions.
- Keep external API compatibility deliberate.

## EF Core and SQL
- Avoid N+1 queries and premature materialization.
- Prefer projections for read models when suitable.
- Use no-tracking queries for read-only work when appropriate.
- Review migrations for existing data and provider differences.
- Keep transactions short and intentional.

## MAUI
- Keep the UI thread responsive.
- Respect lifecycle, navigation, event subscriptions, permissions, and platform differences.
- Measure list/binding performance before broad optimization.
- Treat offline and synchronization behavior explicitly.

## WinForms and DevExpress
- Keep the message loop responsive.
- Handle disposal and event lifetimes carefully.
- Treat designer-generated code conservatively.
- Verify DevExpress APIs against the version actually referenced by the project.

## Testing and validation
- Do not weaken valid tests to make a change pass.
- Test behavior rather than implementation details.
- Use the existing xUnit, NUnit, MSTest, integration, or UI tooling already in the repository.
- Before completion, use `.claude/skills/dotnet-validation/SKILL.md` and run the narrowest meaningful build and test scope.
- Do not assume Node, Vite, Vitest, Tailwind, or Supabase in a .NET-only repository.

## Dependencies
- Inspect project and central package files before adding NuGet packages.
- Prefer existing dependencies and BCL/framework capabilities.
- Do not upgrade unrelated packages as part of a feature or fix.

## Performance and architecture
- Measure before optimizing.
- Avoid repeated database or network calls inside loops when batching is appropriate.
- Keep project dependency direction clear and avoid circular references.
- Do not introduce CQRS, MediatR, repository abstractions, microservices, or extra layers without a concrete repository-specific need.

## AI guardrails
- Inspect code/config before assuming package or framework availability.
- Do not invent version-specific APIs when the referenced version can be checked.
- Do not change tests or quality settings to hide implementation problems.
- Discover answers from the repository when possible instead of asking unnecessary questions.
