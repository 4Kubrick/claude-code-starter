---
name: ask-council
description: Run a structured multi-agent council for consequential architecture, debugging, security, performance, product or technology decisions. Use when the user asks for a council, several expert opinions, a debate, or when a costly-to-reverse decision benefits from independent perspectives.
---

# Ask the Council

Run a focused expert council using Claude Code subagents.

## 1. Frame the decision
Rewrite the request as one concrete decision/review question. Discover constraints from the repository before asking the user.

## 2. Select 3-7 agents
Use the smallest useful panel.

Prefer stack-specific agents when relevant:
- `.NET architecture`: `dotnet-architect`
- `ASP.NET Core / C# backend`: `dotnet-backend`
- `.NET MAUI`: `maui-engineer`
- `WinForms / DevExpress`: `winforms-devexpress`
- `SQL Server/PostgreSQL/SQLite/EF Core`: `database-architect-dotnet`
- `.NET security`: `security-dotnet`
- `.NET operations`: `devops-dotnet`

Also reuse strong upstream agents instead of duplicating them, for example:
- `architecture-strategist`
- `performance-oracle`
- `code-simplicity-reviewer`
- `best-practices-researcher`
- `framework-docs-researcher`
- repository/research agents when evidence is needed

For consequential choices include `devils-advocate`. Use `council-chair` to synthesize.

## 3. Independent round
Ask each selected specialist to analyze the same decision independently. Do not reveal other agents' conclusions during this round.

Each opinion should include:
- recommendation
- evidence/assumptions
- trade-offs
- risks
- confidence

## 4. Challenge round
For important decisions, have the Devil's Advocate attack the leading recommendation. If two specialists materially disagree, ask each to respond to the strongest argument from the other side.

## 5. Synthesis
The chair produces:
1. Decision
2. Why this option wins under current constraints
3. Consensus
4. Disagreements/minority view
5. Risks and mitigations
6. Rejected alternatives and why
7. Concrete next actions
8. Confidence

Do not manufacture consensus. Prefer reversible experiments when evidence is insufficient.