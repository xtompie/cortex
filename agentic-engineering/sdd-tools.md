---
title: Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl
updated: 2026-10-28
tags: [sdd, spec-kit, openspec, kiro, bmad, tessl, tools]
sources:
  - "[github/spec-kit — README](https://github.com/github/spec-kit) — 2026-10-28 — high"
  - "[Spec Kit — command reference](https://github.github.io/spec-kit/reference/agentic-sdd.html) — unknown — high"
  - "[Spec Kit — project history](https://github.github.io/spec-kit/history.html) — unknown — high"
  - "[Fission-AI/OpenSpec — README](https://github.com/Fission-AI/OpenSpec) — 2026-10-28 — high"
  - "[OpenSpec v1.0.0 „The OPSX Release”](https://github.com/Fission-AI/OpenSpec/releases/tag/v1.0.0) — 2026-01-26 — high"
  - "[OpenSpec v1.15.0](https://github.com/Fission-AI/OpenSpec/releases/tag/v1.15.0) — 2026-10-24 — high"
  - "[Kiro — Specs](https://kiro.dev/docs/specs/) — unknown — high"
  - "[Kiro — Feature Specs](https://kiro.dev/docs/specs/feature-specs/) — 2026-08-04 — high"
  - "[Kiro — pricing (przez podsumowanie wyszukiwarki)](https://kiro.dev/pricing/) — unknown — medium"
  - "[bmad-code-org/BMAD-METHOD — README](https://github.com/bmad-code-org/BMAD-METHOD) — 2026-10-14 — high"
  - "[Tessl launches spec-driven framework and registry](https://tessl.io/blog/tessl-launches-spec-driven-framework-and-registry) — 2025-09-16 — medium"
  - "[Tessl Registry](https://tessl.io/registry) — 2026-10-28 — medium"
  - "[Thoughtworks Technology Radar — GitHub Spec Kit](https://www.thoughtworks.com/radar/languages-and-frameworks/github-spec-kit) — 2026-04-15 — high"
  - "[Understanding Spec-Driven-Development (Böckeler)](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) — 2025-10-15 — high"
---

# Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl

> Dwa główne otwarte narzędzia to GitHub Spec Kit (cięższy, z bramkami jakości) i OpenSpec (lżejszy, pod istniejący kod). Kiro to IDE od AWS ze specami w trzech plikach i wymaganiami w stylu EARS. BMAD to pełny proces z personami agentów. Tessl odszedł od SDD w stronę rejestru skilli. Wszystkie działają jako komendy w Twoim agencie (Claude Code, Codex, Copilot, Cursor i inne).

## GitHub Spec Kit

Stan na 2026-10-28: 143 631 gwiazdek, wersja v1.2.5 (2026-10-28). Wydania wychodzą kilka razy w tygodniu.

- Pierwszy commit 21 sierpnia 2025. Od 22 stycznia 2026 głównym maintainerem jest Manfred Riem.
- W 2026 doszły rozszerzenia (luty), presety (marzec) i silnik workflow (kwiecień).
- v1.0.0 (21 sierpnia 2026): „38 coding-agent integrations, 157 community extensions, 33 presets, 270+ contributors”.
- Obecny opis: „Build with a spec, fix a bug, or assess an idea — with your coding agent.” Rdzeń to SDD. Naprawa bugów i ocena pomysłu to dołączane rozszerzenia.

Komendy (nazwa zależy od agenta: `/speckit.<nazwa>` albo `/speckit-<nazwa>`):

| Komenda | Co robi |
|---|---|
| `constitution` | zasady projektu, raz na projekt |
| `specify` | `spec.md` — co i dlaczego |
| `clarify` | „up to five questions” o luki, odpowiedzi trafiają do `spec.md` |
| `plan` | `plan.md` i inne artefakty designu |
| `checklist` | „unit tests for your requirements” |
| `tasks` | `tasks.md` w kolejności zależności |
| `analyze` | kontrola spójności, tylko odczyt |
| `implement` | wykonuje zadania |
| `converge` | sprawdza kod ze spec, planem i zadaniami; może tylko dopisać zadania do `tasks.md` |

Pętla z dokumentacji: „Repeat implement and converge until convergence reports `Converged`.” Komendy uruchamiasz „one at a time, reviewing each result before continuing”.

Instalacja: Python 3.11+ i uv. `uv tool install specify-cli`, potem `specify init my-project --integration copilot` (albo inny agent).

Każdy spec dostaje osobny branch (Böckeler). Thoughtworks Radar trzyma Spec Kit na pierścieniu **Assess** (kwiecień 2026).

## OpenSpec

Stan na 2026-10-28: 73 257 gwiazdek, wersja v1.15.0 (2026-10-24, instalacja bez Node, `openspec update --dry-run`).

Filozofia z README: „fluid not rigid / iterative not waterfall / easy not complex / built for brownfield not just greenfield”.

- v1.0.0 „The OPSX Release” (2026-01-26) zastąpił sztywną sekwencję proposal → apply → archive elastycznymi akcjami. Każdy artefakt można edytować w dowolnym momencie. Komendy `/openspec:proposal`, `/openspec:apply`, `/openspec:archive` usunięto. OpenSpec przestał generować AGENTS.md, zamiast tego instaluje Agent Skills.
- v1.2.0 (2026-02-23): profile i wsparcie Kiro. v1.5.0 (2026-06-28): „Stores Beta” — osobne repo planowania dla funkcji w wielu repozytoriach.
- Wspiera „30+ tools”.

Komendy:
- Profil domyślny: `/opsx:explore`, `/opsx:propose`, `/opsx:apply`, `/opsx:archive`.
- Profil rozszerzony: `/opsx:new`, `/opsx:continue`, `/opsx:ff`, `/opsx:verify`, `/opsx:bulk-archive`, `/opsx:onboard`.
- Zapis zależy od agenta: `/opsx-propose` w Cursor i Copilot, `$openspec-propose` w Codex.

Pliki:
- Zmiana: `openspec/changes/<nazwa>/` z `proposal.md`, `specs/`, `design.md`, `tasks.md`.
- Specy zmiany to delty: `## ADDED Requirements`, `## MODIFIED Requirements`, `## REMOVED Requirements`. Wymagania z SHALL i scenariuszami WHEN/THEN.
- Archive przenosi zmianę do `openspec/changes/archive/YYYY-MM-DD-<nazwa>/` i nanosi delty na główne specy w `openspec/specs/`. Tak `openspec/specs/` zawsze opisuje obecny stan systemu.

README radzi używać modeli z wysokim reasoningiem i „Clear your context before starting implementation.” OpenSpec zbiera anonimową telemetrię. Wyłączysz ją przez `OPENSPEC_TELEMETRY=0`.

## Kiro (AWS)

IDE ze specami. Spec ma trzy pliki: `requirements.md` (albo `bugfix.md`), `design.md`, `tasks.md`.

- Wymagania w formacie EARS: „WHEN [condition/event] THE SYSTEM SHALL [expected behavior]”.
- Feature Spec w dwóch wariantach: Requirements-First (wymagania → design → zadania) albo Design-First (design → wymagania → zadania).
- **Quick Spec** tworzy wszystkie trzy pliki „without approval gates”. Dla dobrze rozumianych funkcji.
- **Bugfix Spec** opisuje obecne, oczekiwane i niezmienione zachowanie.
- „Run all tasks” buduje graf zależności i puszcza niezależne zadania równolegle, falami.
- Modele i ceny znam tylko z podsumowania wyszukiwarki: Claude, GPT-5.6 i modele open-weight. Plany od Pro $20/mies. do Power $200/mies., darmowy plan z 50 kredytami.

## BMAD-METHOD

54 686 gwiazdek. Stabilna linia v6.12 (v6.12.4, 2026-10-14). V7 to „preview alpha”. README podawało termin „October 16, 2026”, ale na 2026-10-28 V7 nie wyszło.

- Opis: „Agile Ai Driven Development” z „Right-sized process — Go directly to implementation for clear changes”.
- Osobne persony agentów: produkt, architektura, UX, dev, test.
- Instalacja: `npx bmad-method install`, potem `bmad-build` i `bmad-help`.

## Tessl

- Start 16 września 2025: Spec Registry (open beta) i Framework (closed beta). Böckeler pisała, że to jedyne narzędzie, które celuje w spec-anchored.
- W 2026 Tessl przeszedł na skille. Strona rejestru mówi teraz: „Version, evaluate, and govern the skills your agents use. Skills are the new code.” Dokładnej daty zmiany nie zweryfikowałem.

## Spory

- OpenSpec nazywa Spec Kit „Thorough but heavyweight. Rigid phase gates, lots of Markdown, Python setup”. Spec Kit 1.x mówi o sobie, że procesy to „independent entry points, not mandatory phases”. OpenSpec sam porzucił sztywną sekwencję w v1.0.
- OpenSpec pisze, że Kiro jest „limited to Claude models”.

> **Status: Outdated** (2026-10-28) — cennik Kiro (według podsumowania wyszukiwarki) wymienia też GPT-5.6 i modele open-weight.

## Jak stosować

Wybór narzędzia (decyzja Cortexu na podstawie źródeł wyżej):

1. **Mała zmiana, bug** — bez narzędzia SDD. Plan w czacie albo Quick Spec w Kiro.
2. **Zmiana w istniejącym repo, chcesz lekko** — OpenSpec:
   1. `openspec init` w repo.
   2. `/opsx:explore` — rozpoznanie.
   3. `/opsx:propose <zmiana>` — przeczytaj `proposal.md` i delty speców. Popraw je.
   4. Wyczyść kontekst (`/clear`), potem `/opsx:apply`.
   5. `/opsx:archive` — delty trafiają do `openspec/specs/`.
3. **Duża funkcja, chcesz bramki jakości** — Spec Kit: `constitution` raz, potem `specify` → `clarify` → `plan` → `checklist`/`analyze` → `tasks` → `implement` ↔ `converge`. Po każdym kroku czytaj wynik.
4. **Pracujesz w IDE i chcesz wymagań EARS** — Kiro. Requirements-First dla funkcji produktowych, Design-First przy twardych wymaganiach niefunkcjonalnych.
5. **Chcesz cały proces zwinny z rolami** — BMAD v6.12. Nie bierz V7 alpha, jeśli nie zniesiesz zmian łamiących zgodność.

## Zobacz też
- [Spec-driven development (SDD)](spec-driven-development.md) — czym jest SDD, poziomy, krytyka, dowody
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — gdzie SDD pasuje w codziennym procesie
- [Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md) — OpenSpec i Tessl przeszły na skille
- [Spec-driven development — OpenSpec, Spec Kit, BMAD, Open Mercato](../ai-news/spec-driven-tools.md) — nowości i wydania tych narzędzi oraz Open Mercato
