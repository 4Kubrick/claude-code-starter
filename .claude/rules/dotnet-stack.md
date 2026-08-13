# .NET Stack Routing

When a repository contains `.sln`, `.slnx`, `.csproj`, C# or XAML, use the .NET path.

## Specialists
- Architecture: `dotnet-architect`
- ASP.NET Core and C#: `dotnet-backend`
- .NET MAUI: `maui-engineer`
- WinForms and DevExpress: `winforms-devexpress`
- EF Core and databases: `database-architect-dotnet`
- Operations and deployment: `devops-dotnet`

Generic upstream agents remain useful for repository research, performance, simplicity, and documentation.

## Implementation Units
The upstream builder names are intentionally retained and repurposed for .NET in this fork:
- backend/data: `feature-builder-data`
- MAUI, WinForms, DevExpress, or Blazor UI: `feature-builder-ui`
- cross-layer .NET work: `feature-builder-fullstack`

Do not use React/Tailwind/Supabase-specific skills for .NET-only work. Use them only when those technologies are actually present in the changed scope.

## Validation
Use `dotnet-validation`. Build the narrowest relevant project or solution and run targeted tests. Treat native MAUI and WinForms UI smoke checks separately from compilation.

## Council
Use `ask-council` for important multi-discipline decisions and keep the panel focused.
