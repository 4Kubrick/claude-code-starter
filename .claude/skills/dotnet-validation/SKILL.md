---
name: dotnet-validation
description: Validate .NET changes using the repository's actual solution, target frameworks, tests, analyzers and platform requirements. Use before declaring .NET work complete.
---

# .NET Validation

## Discover before running
Find the actual build entry point:
- `.sln` / `.slnx`
- `.csproj`
- `Directory.Build.props`
- `Directory.Packages.props`
- test projects
- CI workflow/build scripts

Determine whether the repo is backend, MAUI, WinForms/DevExpress, Blazor, or mixed .NET + JS.

## Default gate
Use the narrowest gate that proves the change:

```bash
dotnet build <solution-or-project>
dotnet test <relevant-test-project-or-solution> --no-build
```

Run `dotnet restore` first only if dependencies/assets require it. Use the repo's configuration/framework flags when present.

If analyzers/formatting are configured, run the configured command. Do not add a formatter just to satisfy this skill.

## Platform rules
- ASP.NET Core: build + unit/integration tests; exercise API boundary when the change affects auth/data/contracts.
- MAUI: build the relevant target when the environment supports it; otherwise report the unavailable platform gate explicitly. Add manual smoke steps for native UI changes when no automation exists.
- WinForms/DevExpress: build the actual Windows target; run tests and explicit manual smoke steps for UI behavior when no harness exists.
- Blazor/web: add browser smoke/E2E when a runnable web UI and tooling exist.

## Mixed repositories
If the changed scope includes a JS frontend, validate that frontend with its own package scripts. Do not assume Vite/Vitest/Tailwind; read `package.json`.

## Failure policy
- Fix production code rather than weakening valid tests.
- Do not change analyzer/test configuration to hide a failure.
- Distinguish environment/tooling blockers from code defects.
- Report exactly which gate was run and which could not be run.
