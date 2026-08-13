---
name: dev-docs-execute
description: "Kontynuacja pracy nad zadaniem - wykonanie kolejnej fazy/etapu z walidacją dopasowaną do rzeczywistego stacku repo."
argument-hint: "[ścieżka-do-folderu np. 'docs/active/auth-refaktor']"
---

# Wykonanie kolejnej fazy zadania

## Wykonanie
Ustal `sciezka` (folder zadania w `docs/active/`) i `faza` (numer fazy). Jeśli `faza` nie została podana jawnie, wylicz pierwszą nieukończoną fazę z `$sciezka/*-zadania.md`.

Uruchom workflow:

```text
Workflow({scriptPath: ".claude/workflows/dev-docs-execute-wf.js", args: {sciezka, faza}})
```

Po zakończeniu streść: fazę, status, IU, commity, wynik walidacji i odchylenia.

## 1. Zasada nadrzędna: wykryj stack
Przed delegacją i przed końcowym gate ustal stack z repozytorium, nie z tego startera.

Dla .NET sprawdź przede wszystkim:
- `.sln` / `.slnx`
- `.csproj` i `TargetFramework*`
- `Directory.Build.props` / `Directory.Packages.props`
- test projects
- CI/build scripts
- MAUI/WinForms/Blazor/ASP.NET markers

Jeśli target repo jest .NET-only, reguły `.claude/rules/dotnet-stack.md` oraz skill `dotnet-validation` mają pierwszeństwo nad legacy przykładami Vite/Vitest obecnymi w workflow JS.

## 2.5 Strategia delegacji
Każdy Implementation Unit powinien być wykonywany przez subagenta z `Delegate to:`.

- `feature-builder-data` — backend/data/integration .NET
- `feature-builder-ui` — MAUI / WinForms / DevExpress / Blazor UI
- `feature-builder-fullstack` — cross-layer .NET

### Serial
Użyj, gdy IU mają zależności, wspólne pliki, migracje lub zmiany pakietów/build configuration.

### Parallel
Użyj tylko dla naprawdę niezależnych IU bez wspólnego stanu i ordering constraints.

### Inline fallback
Tylko dla legacy IU bez `Delegate to:` albo trywialnej poprawki. Nie omijaj subagentów dla normalnej implementacji.

## 3. Kontekst dla buildera
Prompt buildera zawiera cały IU: Cel, Wymagania, Pliki, Podejście, Wzorce, Scenariusze testowe, Weryfikacja, ścieżkę zadania i numer IU.

Dodatkowo builder powinien przeczytać:
- `docs/CONCEPTS.md`, jeśli istnieje
- `.claude/rules/learned-patterns.md`, jeśli istnieje
- `.claude/rules/dotnet-stack.md` dla repo .NET

### Designerski kontekst
Dla UI/fullstack dołącz DESIGN.md / SPEC.md / referencyjne screeny, jeśli projekt je posiada. Nie zakładaj, że UI jest web/Tailwind. SPEC/design jest opisem wyglądu; implementacja musi użyć frameworka faktycznie obecnego w repo (MAUI XAML, WinForms/DevExpress, Blazor itd.).

## 4. Obsługa raportów
- `completed` — kontynuuj
- `partial` — oceń, czy wymaga zmiany planu; jeśli tak, zatrzymaj fazę
- `blocked` — zatrzymaj i przedstaw konkretny blocker

Odchylenia zmieniające scope muszą zostać zapisane i świadomie zaakceptowane przed rozszerzeniem pracy.

## 4.5 System-Wide Test Check
Przed zamknięciem fazy odpowiedz:
1. Czy właściwy build/type gate dla TEGO STACKU przechodzi?
2. Czy istniejące relevant testy przechodzą?
3. Czy nowe testy pokrywają happy path i istotny failure/edge case?
4. Czy nowe zależności/referencje nie łamią solution/project boundaries?
5. Czy platform/integration gate wymagany przez zmianę został wykonany albo jawnie oznaczony jako niedostępny środowiskowo?

### .NET default
Użyj `dotnet-validation`. Typowo:

```bash
dotnet build <solution-or-project>
dotnet test <relevant-tests> --no-build
```

Uruchom restore tylko gdy potrzebny. Użyj repozytoryjnych flags/configuration/TFM. Jeśli analyzers/formatter są skonfigurowane, uruchom je.

### MAUI
Build relevant target, jeśli środowisko go wspiera. Dla natywnego UI bez harnessu dodaj jawny manual smoke zamiast udawać browser E2E.

### WinForms / DevExpress
Build Windows target + tests; UI smoke może wymagać operatora. Brak przeglądarki nie jest błędem.

### Mixed .NET + JS
Waliduj część JS tylko jeśli zmiana jej dotyczy i użyj komend z jej `package.json`. Nie zakładaj Vite/Vitest.

## 5. Scope
Wykonaj tylko jedną fazę. Nie wykonuj checkboxów `Weryfikacja:` jako implementacji. Nie przechodź automatycznie do kolejnej fazy.
