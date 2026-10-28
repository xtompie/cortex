---
title: Jak przygotować repo i agenta do pracy
updated: 2026-10-28
tags: [process, setup, agents-md, skills, output-style, hooks]
sources:
  - "[AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md)"
  - "[Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md)"
  - "[Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty](agent-communication-style.md)"
  - "[Context engineering dla agentów kodujących](context-engineering.md)"
  - "[Claude Code — Extend Claude Code (features overview)](https://code.claude.com/docs/en/features-overview) — unknown — high"
  - "[Writing a good CLAUDE.md (HumanLayer)](https://www.humanlayer.dev/blog/writing-a-good-claude-md) — 2025-11-25 — medium"
  - "[Agentic Coding Recommendations (Armin Ronacher)](https://lucumr.pocoo.org/2025/6/12/agentic-coding/) — 2025-06-12 — high"
---

# Jak przygotować repo i agenta do pracy

> Przygotowanie ma pięć warstw: krótki plik instrukcji, szybkie komendy do sprawdzania, hooki na rzeczy obowiązkowe, skille na powtarzalne procedury i styl komunikacji. Zaczynasz od minimum i dokładasz tylko wtedy, gdy agent popełnia ten sam błąd drugi raz.

## Kroki

### 1. Szybka pętla sprawdzania
- Jedna komenda na testy, jedna na lint i typy. Agent musi umieć sam sprawdzić swoją pracę.
- Ronacher: „Tools need to be fast”. „Crashes are tolerable; hangs are problematic”.

### 2. Plik instrukcji
- `AGENTS.md` jako główny. `CLAUDE.md` z linią `@AGENTS.md`, jeśli używasz Claude Code ([AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md)).
- Na start: komendy z kroku 1, nietypowe narzędzia, nietypowe konwencje, krótka mapa katalogów.
- Poniżej 200 linii. Bez stylu kodu, bez opisu architektury, który agent wyczyta z kodu.

### 3. Hooki i uprawnienia na rzeczy obowiązkowe
- Formatter w hooku, nie w instrukcji (HumanLayer).
- Zakazy (np. pliki `.env`, push) przez uprawnienia albo hook `PreToolUse`. Instrukcja „is a request, not a guarantee” (Claude Code).

### 4. Skille na powtarzalne procedury
- Trzeci raz wklejasz tę samą instrukcję → skill ([Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md)).
- Skille z efektem ubocznym tylko na ręczne wywołanie.
- Skille z zewnątrz tylko z zaufanych źródeł, po przejrzeniu skryptów.

### 5. Styl komunikacji
- Output style raz dla wszystkich projektów. Własny styl z `keep-coding-instructions: true` ([Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty](agent-communication-style.md)).
- W stylu: wynik na początku, dowód z sesji przy każdym twierdzeniu, „nie wiem” dozwolone.

### 6. Utrzymanie (decyzja Cortexu)
- Agent powtórzył błąd → jedna linia w AGENTS.md albo nowy hook.
- Raz na kilka tygodni: przejrzyj AGENTS.md pod kątem sprzeczności i nieaktualnych reguł. W Claude Code: `/doctor prompt-audit`.
- Po zmianie modelu: przejrzyj styl komunikacji i długie instrukcje.

## Pytania do usera przed konfiguracją (decyzja Cortexu)
- Jakich agentów używasz (Claude Code, Codex, Cursor)? Od tego zależy nazwa pliku i miejsce skilli.
- Jakie komendy sprawdzają poprawność w tym repo?
- Czego agent nie może ruszać nigdy?
- Jakie procedury powtarzasz co tydzień?

## Zobacz też
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — praca nad zadaniem po przygotowaniu
- [Context engineering dla agentów kodujących](context-engineering.md) — dlaczego minimum
