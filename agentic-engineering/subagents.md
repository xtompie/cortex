---
title: Subagenty i praca wieloagentowa
updated: 2026-10-28
tags: [subagents, multi-agent, context-engineering, claude-code, codex]
sources:
  - "[Claude Code — Subagents](https://code.claude.com/docs/en/sub-agents) — unknown — high"
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[How we built our multi-agent research system (Anthropic)](https://www.anthropic.com/engineering/multi-agent-research-system) — 2025-06-13 — high"
  - "[Effective context engineering for AI agents (Anthropic)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — 2025-09-29 — high"
  - "[Don't Build Multi-Agents (Cognition, Walden Yan)](https://cognition.com/blog/dont-build-multi-agents) — 2025-06-12 — high"
  - "[Multi-Agents: What's Actually Working (Cognition)](https://cognition.com/blog/multi-agents-working) — 2026-04-22 — high"
  - "[Agentic Engineering Patterns — Subagents (Simon Willison)](https://simonwillison.net/guides/agentic-engineering-patterns/subagents/) — unknown — high"
  - "[Advanced Context Engineering for Coding Agents (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md) — unknown — medium"
  - "[Codex — Subagents (OpenAI)](https://learn.chatgpt.com/docs/agent-configuration/subagents) — unknown — high"
---

# Subagenty i praca wieloagentowa

> Subagent to osobny agent z własnym oknem kontekstu. Dostaje zadanie i zwraca streszczenie. Daje dwie rzeczy: czysty kontekst główny i świeże oko. Nie daje mądrzejszej odpowiedzi. Kosztuje więcej tokenów. Zasada z praktyki 2026: czytać może wielu agentów naraz, pisać powinien jeden.

## Co to jest

- Claude Code: „Each subagent runs in its own context window with a custom system prompt, specific tool access, and independent permissions.”
- Wbudowane w Claude Code: Explore (tylko odczyt), Plan (tylko odczyt), general-purpose. Zagnieżdżenie do trzech poziomów pod główną rozmową. Subagenty startują domyślnie w tle. Tryb fork (dziedziczy rozmowę rodzica) jest domyślnie włączony.
- Codex: wbudowane `default`, `worker`, `explorer`. Własne agenty to pliki TOML w `.codex/agents/`.
- Subagent zwraca „a condensed, distilled summary of its work (often 1,000-2,000 tokens)” (Anthropic).

## Kiedy używać

Claude Code — subagent, gdy:
- „The task produces verbose output you don't need in your main context”,
- chcesz ograniczyć narzędzia (np. recenzent tylko z `Read, Grep, Glob`),
- „The work is self-contained and can return a summary”.

Claude Code — główna rozmowa, gdy:
- „Multiple phases share significant context”,
- zmiana jest „quick, targeted”,
- „Latency matters”.

Codex: równolegle „for read-heavy tasks such as exploration, tests, triage, and summarization”. „Be more careful with parallel write-heavy workflows”.

HumanLayer: „Subagents are about context control.” Główne użycie to „znajdź i streść” w świeżym oknie.

## Czego subagent nie daje

- Claude Code: „Handing the same task to a subagent doesn't make the answer any better.” „You get parallelism or a fresh pair of eyes out of it, but not a smarter answer.”
- Subagent może być wolniejszy, bo musi od nowa zebrać kontekst.
- Willison: „Your root coding agent is perfectly capable of debugging or reviewing its own output provided it has the tokens to spare.” Ostrzega przed „dozens of different specialist subagents”.
- Wyjątek: świeży recenzent pomaga, bo nie widział rozumowania, które stworzyło kod ([Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md)).

## Koszt

- Anthropic (system research): agenci zużywają ok. 4× więcej tokenów niż czat, systemy wieloagentowe ok. 15×. Ilość tokenów tłumaczy 80% wariancji wyniku na BrowseComp.
- Codex: „subagent workflows consume more tokens than comparable single-agent runs”.

## Spór o wiele agentów

- **Anthropic (czerwiec 2025)** — Opus 4 jako lider z subagentami Sonnet 4 wygrał z pojedynczym Opus 4 o 90,2% na wewnętrznym teście researchu. Ale „most coding tasks involve fewer truly parallelizable tasks than research.”
- **Cognition (czerwiec 2025)** — „Don't Build Multi-Agents”. Zasady: „Share context, and share full agent traces, not just individual messages” oraz „Actions carry implicit decisions, and conflicting decisions carry bad results”. Równoległe subagenty w przykładzie z Flappy Bird zrobiły niepasujące do siebie style.
- **Cognition (kwiecień 2026)** — rewizja: „writes stay single-threaded and the additional agents contribute intelligence rather than actions”. Działa układ: menedżer dzieli pracę, dzieci wykonują, menedżer składa wynik. Swobodne roje to „mostly a distraction”.
- Claude Code i Codex domyślnie uruchamiają dziś subagenty. To idzie dalej niż ostrożność Cognition.

## Jak stosować

1. Subagent do: przeszukania repo, researchu w sieci, czytania logów, review. Do głównej sesji ma wrócić krótki raport.
2. Pisze jeden agent. Równoległe zmiany w kodzie tylko w osobnych worktree i na rozłącznych kawałkach ([Agenci równolegle — worktree, praca w tle, headless](parallel-agents.md)).
3. Prompt subagenta musi być samodzielny: cel, co już wiesz, czego nie robić, format i długość raportu. Subagent nie widzi Twojej rozmowy, chyba że to fork.
4. Recenzenta ogranicz do narzędzi tylko do odczytu.
5. Proste zadania daj tańszemu modelowi (np. Haiku). Sprawdzaj zużycie (`/usage`).
6. Nie twórz kolekcji wyspecjalizowanych person „na zapas”.

## Zobacz też
- [Context engineering dla agentów kodujących](context-engineering.md) — po co izolować kontekst
- [Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md) — recenzja w świeżym kontekście
- [Agenci równolegle — worktree, praca w tle, headless](parallel-agents.md) — worktree i praca równoległa
