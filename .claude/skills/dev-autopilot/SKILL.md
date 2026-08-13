---
name: dev-autopilot
description: Execute an approved implementation plan. In .NET repositories use the .NET-first implementation and validation path.
---

# Dev Autopilot

First detect the repository stack.

## .NET repositories

If `.sln`, `.slnx`, `.csproj` or C# projects are present, follow `.claude/rules/dotnet-stack.md` and `CLAUDE.md`.

For each approved phase:
1. Inspect the relevant solution/project and existing conventions.
2. Select the appropriate .NET specialist (`dotnet-backend`, `maui-engineer`, `winforms-devexpress`, `database-architect-dotnet`, etc.).
3. Implement only the phase scope.
4. Validate with the narrowest relevant .NET build/tests.
5. Review using relevant .NET agents plus generic `performance-oracle`, `code-simplicity-reviewer`, `security-sentinel` or `architecture-strategist` when useful.
6. Fix concrete defects and repeat affected validation.
7. Update task documentation with decisions and remaining manual validation.

Do not use Vite/Vitest/Supabase-specific workflow assumptions for a .NET repository.

## Non-.NET repositories

Use the original upstream workflow conventions and stack-specific skills available in the repository.

For expensive-to-reverse architecture or migration choices, invoke `/ask-council` before implementation.