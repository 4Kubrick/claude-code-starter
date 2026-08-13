---
name: dotnet-validation
description: Validate .NET changes using the repository's actual solution, target frameworks, tests, analyzers, and platform requirements.
---

# .NET Validation

Discover the real build entry point first: `.sln`, `.slnx`, `.csproj`, central build/package files, test projects, and CI scripts.

Use the narrowest validation that proves the change. A typical sequence is:

```bash
dotnet build <solution-or-project>
dotnet test <relevant-test-project-or-solution> --no-build
```

Run restore only when required. Respect repository configuration and target framework settings. Run analyzers or formatting only when the repository already configures them.

For ASP.NET Core, include relevant integration checks when API contracts, data, or authorization change. For MAUI, build the relevant target when the environment supports it and report native manual smoke steps when UI automation is absent. For WinForms/DevExpress, build the real Windows target and use existing tests plus manual UI smoke where necessary.

If a separate JavaScript frontend is part of the changed scope, validate it with its own package scripts. Do not assume Vite or Vitest.

Report exactly which checks ran and which could not run in the current environment.
