---
name: dev-docs-execute
description: Execute the next phase of an approved task using the repository's actual technology stack.
argument-hint: "[path-to-task-folder]"
---

# Execute next phase

Determine the task folder and the first incomplete phase from the task documents.

## .NET repositories
If the repository contains `.sln`, `.slnx`, `.csproj`, C# or XAML, do not use the legacy JavaScript execution workflow. Execute the phase directly with the .NET path below.

1. Read the task plan, context, technical plan, `CLAUDE.md`, `.claude/rules/dotnet-stack.md`, and learned project rules when present.
2. Execute only one phase.
3. Delegate each Implementation Unit using its `Delegate to:` value. Use the .NET-aware builders:
   - `feature-builder-data`
   - `feature-builder-ui`
   - `feature-builder-fullstack`
4. Use serial execution when IUs share files, migrations, packages, or ordering constraints. Use parallel execution only for independent IUs.
5. If a builder reports partial or blocked work, stop the phase and report the concrete remaining issue instead of expanding scope.
6. Validate the completed phase with `dotnet-validation`.
7. Update the task checklist and context with completed work, decisions, validation results, and remaining manual UI checks.
8. Do not start the next phase.

For UI/fullstack IUs, include available DESIGN/SPEC/reference screens, but implement them using the actual framework in the repository rather than assuming a web stack.

## Non-.NET repositories
Keep compatibility with the upstream starter by using:

```text
Workflow({scriptPath: ".claude/workflows/dev-docs-execute-wf.js", args: {sciezka, faza}})
```

Then summarize the workflow result.

## Completion gate for .NET
A phase is complete only when the relevant build and tests pass, or when an unavailable platform-specific check is clearly reported as a manual/environment step. Do not substitute Node/Vite/Vitest checks for a .NET-only solution.
