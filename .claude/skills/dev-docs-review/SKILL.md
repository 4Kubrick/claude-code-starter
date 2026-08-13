---
name: dev-docs-review
description: Review the current implementation phase using checks matched to the repository's actual stack.
argument-hint: "[path-to-task-folder]"
---

# Review current phase

Read the task plan, context, changed files, and phase scope first.

## .NET repositories
If the repository contains `.sln`, `.slnx`, `.csproj`, C# or XAML, review the phase directly instead of using the legacy JavaScript review workflow.

Select only reviewers relevant to the changed scope:
- `dotnet-architect` for solution structure
- `dotnet-backend` for ASP.NET Core and C#
- `maui-engineer` for MAUI
- `winforms-devexpress` for WinForms and DevExpress
- `database-architect-dotnet` for persistence
- `performance-oracle` for performance
- `code-simplicity-reviewer` for unnecessary complexity
- `feature-tester-e2e` for web or native smoke scenarios

Deduplicate overlapping observations and keep the review focused on the requested phase. Validate the affected projects with `dotnet-validation`. For native UI, keep build/test evidence separate from manual smoke steps.

Record the review result in the task documentation: important findings, validation result, remaining manual checks, and concrete follow-up work.

Use `ask-council` only when the phase contains an important multi-discipline decision.

## Non-.NET repositories
Keep upstream compatibility by using:

```text
Workflow({scriptPath: ".claude/workflows/dev-docs-review-wf.js", args: {sciezka, faza}})
```

Then summarize the workflow result.
