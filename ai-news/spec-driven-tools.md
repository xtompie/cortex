---
title: Spec-driven development — OpenSpec, Spec Kit, BMAD, Open Mercato
updated: 2026-10-28
tags: [sdd, spec-driven, openspec, spec-kit, bmad, open-mercato]
sources:
  - "[Fission-AI/OpenSpec — README](https://github.com/Fission-AI/OpenSpec) — 2026-10-28 — high"
  - "[github/spec-kit — README](https://github.com/github/spec-kit) — 2026-10-28 — high"
  - "[bmad-code-org/BMAD-METHOD — GitHub](https://github.com/bmad-code-org/BMAD-METHOD) — 2026-10-28 — medium"
  - "[open-mercato/open-mercato — README](https://github.com/open-mercato/open-mercato) — 2026-10-28 — high"
---

# Spec-driven development — OpenSpec, Spec Kit, BMAD, Open Mercato

> Spec-driven development (SDD): agent najpierw pisze specyfikację (wymagania, scenariusze, projekt techniczny, lista zadań), człowiek ją zatwierdza, a dopiero potem agent koduje. Dwa najpopularniejsze narzędzia to Spec Kit od GitHuba (★144k) i OpenSpec (★73k). OpenSpec jest lżejszy i lepszy do istniejących projektów. Spec Kit to rozbudowany zestaw procesów z rozszerzeniami i katalogami.

## OpenSpec (Fission-AI)

- ★73k, MIT. Stan: `v1.15.0` z 2026-10-24.
- Filozofia: płynnie, iteracyjnie, prosto, „built for brownfield not just greenfield”.
- Cykl komend:
  1. `/opsx:explore`: rozmowa o pomyśle, agent czyta kod.
  2. `/opsx:propose <nazwa>`: tworzy `openspec/changes/<nazwa>/` z `proposal.md`, `specs/`, `design.md`, `tasks.md`.
  3. `/opsx:apply`: implementacja zadań z `tasks.md`.
  4. `/opsx:archive`: przeniesienie do archiwum i aktualizacja głównych specyfikacji.
- Specyfikacje to zwykły Markdown: wymagania z „SHALL” i scenariusze WHEN/THEN.

## Spec Kit (GitHub)

- ★144k, MIT. Stan: `v1.2.5` z 2026-10-28. Wydania prawie codziennie.
- Od wersji 1.x to nie jeden proces, tylko zestaw procesów:
  - Spec-Driven Development, w rdzeniu: specyfikacja, potem plan, implementacja i „convergence”;
  - Bug fixing, jako rozszerzenie: ocena przyczyny, wąska poprawka, zapis weryfikacji;
  - Idea assessment, jako rozszerzenie: decyzja go, clarify albo stop na podstawie dowodów.
- Mechanizmy: integracje z agentami, rozszerzenia, hooki, presety (np. standardy firmowe), workflowy, bundle i katalogi komponentów, także prywatne.
- Wymaga Pythona 3.11+ i `uv`. CLI nazywa się `specify`.
- Uwaga z README: wpisy w katalogach społeczności nie są audytowane. Przejrzyj kod, zanim zainstalujesz.

## BMAD-METHOD

- ★55k. „Breakthrough Method for Agile AI Driven Development”. Opisuje role agentów (analityk, PM, architekt, dev) i przekazywanie dokumentów między nimi. Jest cięższy od OpenSpec.

## Open Mercato

To prawdopodobnie „Open Mencarto”, o które pytałeś. Pewności nie mam.

- `open-mercato/open-mercato` (★1.9k, MIT, `v0.9.0` z 2026-10-09). Framework TypeScript na Next.js i PostgreSQL do aplikacji biznesowych: CRM, ERP, commerce i magazyn.
- Zbudowany pod agentów kodujących. Każda aplikacja ma `AGENTS.md` i skille, które mówią agentowi, gdzie trafia kod, moduły i UI.
- Spec-first: specyfikacje leżą obok kodu w `.ai/specs/`. Agent planuje, człowiek zatwierdza, potem jest implementacja.
- **Cezar**: agent, który uruchamia te same skille równolegle, według harmonogramu albo na zdarzenia GitHuba. Nigdy sam nie merguje.
- Start: `npx create-mercato-app my-app --preset classic --agents all --init-git`. Jest też Open Mercato Cloud w przeglądarce, w becie.
- Osobne repo `open-mercato/skills` zawiera skille „Enterprise AI Engineering”. Według opisu powstały przy ERP z ponad 1,2 mln linii kodu napisanym z AI.

## Jak stosować

- Mały i średni projekt, zmiany w istniejącym kodzie → **OpenSpec**. Najmniej narzutu, cztery komendy.
- Zespół albo potrzeba standardów firmowych, gotowych procesów do bugów i oceny pomysłów → **Spec Kit**.
- Aplikacja biznesowa od zera (CRM/ERP) z agentami → przejrzyj **Open Mercato** jako gotowy fundament.
- Niezależnie od narzędzia: specyfikacja z konkretnymi scenariuszami WHEN/THEN daje agentowi kryterium „gotowe”.

## Zobacz też
- [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md) — agenci, z którymi te narzędzia współpracują
- [Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl](../agentic-engineering/sdd-tools.md) — jak pracować z tymi narzędziami i które wybrać
