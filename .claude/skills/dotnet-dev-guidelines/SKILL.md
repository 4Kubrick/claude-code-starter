---
name: dotnet-dev-guidelines
description: Apply pragmatic modern .NET engineering guidance for ASP.NET Core, EF Core, MAUI, WinForms/DevExpress and background/integration services.
---

# .NET Development Guidelines

## First principle
Use the architecture and conventions already present in the target repository. This skill specializes implementation quality; it does not authorize a rewrite.

## C# / runtime
- Respect the target framework and language version.
- Use nullable reference types intentionally.
- Avoid sync-over-async and `async void` outside event handlers.
- Propagate cancellation through I/O where meaningful.
- Dispose resources deterministically.

## ASP.NET Core
- Validate at boundaries and authorize server-side.
- Use correct DI lifetimes.
- Keep external contracts deliberate and backwards-compatible when required.
- Use consistent error responses and structured logging.

## EF Core / SQL
- Avoid N+1 and premature materialization.
- Prefer projections for read models.
- Use `AsNoTracking` for suitable reads.
- Review migration impact on existing production data.
- Treat SQL Server, PostgreSQL and SQLite provider differences explicitly.

## MAUI
- Protect UI-thread responsiveness.
- Watch lifecycle, event subscriptions and memory retention.
- Measure CollectionView/binding performance instead of guessing.
- Define offline/reconnect/conflict behavior explicitly.

## WinForms / DevExpress
- Protect the message loop and UI thread.
- Be conservative with stable legacy code.
- Verify version-specific DevExpress APIs during upgrades.
- Treat designer-generated code and disposal/event lifetimes carefully.

## Distributed/background work
For SignalR, RabbitMQ, Quartz.NET and hosted services, reason about retries, idempotency, duplicate delivery, shutdown and observability.

## Architecture restraint
Do not add CQRS, MediatR, repository patterns, DDD layers, microservices or generic abstractions without a concrete problem they solve in this repository.
