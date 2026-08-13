---
name: dotnet-dev-guidelines
description: Apply pragmatic modern .NET engineering guidance for ASP.NET Core, EF Core, MAUI, WinForms/DevExpress, and integration services.
---

# .NET Development Guidelines

Use the architecture and conventions already present in the target repository. This skill improves implementation quality; it does not authorize a rewrite.

- Respect the target framework and C# language version.
- Use nullable reference types intentionally.
- Keep asynchronous I/O asynchronous and pass cancellation where useful.
- Use correct ASP.NET Core dependency injection lifetimes and existing API conventions.
- For EF Core, avoid N+1 queries and unnecessary materialization; review migration impact on existing data.
- For MAUI, protect UI responsiveness, lifecycle, navigation, and event subscriptions.
- For WinForms/DevExpress, protect the message loop, disposal, designer files, and version-specific APIs.
- For SignalR, RabbitMQ, Quartz.NET, and hosted services, consider retries, duplicate work, shutdown, and observability.
- Do not add CQRS, MediatR, repository layers, microservices, or generic abstractions unless they solve a concrete problem in this repository.
