---
title: Hermes Agent (Nous Research)
updated: 2026-10-28
tags: [hermes, agent, memory, self-improving, nous-research]
sources:
  - "[NousResearch/hermes-agent — README](https://github.com/NousResearch/hermes-agent) — 2026-10-28 — high"
  - "[eesel.ai — Hermes AI agent review](https://www.eesel.ai/blog/hermes-agent-review) — 2026 — medium"
  - "[AgentConn — Is Self-Improving AI a Real Category?](https://agentconn.com/blog/nousresearch-hermes-agent-self-improving-framework-review/) — 2026 — medium"
  - "[Medium — Hermes Agent Desktop App](https://medium.com/@tentenco/hermes-agent-desktop-app-everything-you-need-to-know-about-nous-researchs-self-improving-ai-agent-3cb59bd31e5f) — 2026 — low"
---

# Hermes Agent (Nous Research)

> Hermes Agent to otwarty agent osobisty od Nous Research, MIT, ★258k. Działa na dowolnym modelu. Wyróżnia go pętla uczenia: sam tworzy skille z doświadczenia, poprawia je w trakcie, pamięta rozmowy między sesjami i buduje model użytkownika. Działa na serwerze (nawet VPS za 5 USD), a rozmawiasz z nim przez Telegram, Slack, Discord, WhatsApp, Signal albo CLI.

## Co to jest

- Autor: Nous Research, znany z otwartych modeli Hermes. Repo od 2025-07-22. Według recenzji publiczny start był w lutym 2026.
- Stan na 2026-10-28: `v0.22.5` z 2026-10-23. Wydania co kilka dni.
- Instalacja: `curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`, potem `hermes`. Jest też natywny Windows, Termux i aplikacja Hermes Desktop. Desktop wyszedł według bloga 2 czerwca 2026.

## Funkcje (z README)

- **Pętla uczenia:** pamięć prowadzona przez agenta, automatyczne skille po złożonych zadaniach, wyszukiwanie w dawnych sesjach (FTS5 + streszczenia LLM), model użytkownika przez Honcho. Zgodny ze standardem skilli agentskills.io.
- **Harmonogram:** wbudowany cron. Raporty dzienne, kopie, audyty w języku naturalnym, wysyłane na dowolną platformę.
- **Subagenty** do równoległej pracy. Skrypty Pythona wywołują narzędzia przez RPC, żeby nie zużywać kontekstu.
- **Backendy terminala:** lokalny, Docker, SSH, Modal, Daytona, Vercel Sandbox. Modal i Daytona usypiają środowisko, gdy agent nic nie robi.
- **Dowolny model:** Nous Portal, OpenRouter, OpenAI, własny endpoint. Zmiana przez `hermes model`.

## Dlaczego jest popularny

- Rozwiązuje problem, którego nie rozwiązują Claude Code ani Cursor: pamięć i praca asynchroniczna między sesjami.
- Darmowy, self-hosted, bez opłat za stanowisko.
- Zaufanie do Nous Research z czasów modeli Hermes.
- Liczby wzrostu (np. 175k gwiazdek w niecałe 4 miesiące, wycena 1,5 mld USD) pochodzą od firmy albo z blogów. Nikt ich niezależnie nie sprawdził.

## Krytyka

- Trudna instalacja dla nietechnicznych osób.
- Skille napisane przez agenta trzeba przejrzeć, zanim pójdą na produkcję.
- Sam agent jest darmowy, ale modele w chmurze kosztują.

## Podobny projekt: OpenClaw

`openclaw/openclaw` (★393k, MIT, od 2025-11-24) to inny osobisty asystent na własnym sprzęcie. Działa w 20+ komunikatorach (Discord, iMessage, Slack, Teams, Telegram, WhatsApp) i ma aplikacje na macOS, iOS, Androida, Windows i Linuksa. Stan, pamięć i dane logowania zostają na Twoim sprzęcie. Modele i harnessy (Claude, Codex, lokalne) to wymienne pluginy. Wersje mają format daty, np. `v2026.10.8`.

Różnica: Hermes stawia na samodoskonalenie i pracę na serwerze. OpenClaw stawia na obecność we wszystkich komunikatorach i urządzeniach.

## Jak stosować

- Warto spróbować, jeśli chcesz agenta, który działa 24/7 i pisze do Ciebie na Telegramie, np. z codziennym raportem.
- Start: postaw go na tanim VPS albo w Dockerze, podłącz model przez OpenRouter i jeden komunikator. Pierwsze zadanie daj z cronem.
- Przeglądaj skille, które agent sam tworzy.
- Do pracy nad kodem w repo dalej lepszy jest agent kodujący. Hermes jest uzupełnieniem.

## Zobacz też
- [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md) — agenci kodujący pracujący w sesjach
- [Pamięć dla agentów — Mem0, Letta, Zep/Graphiti, Honcho, Graphify](agent-memory.md) — biblioteki pamięci dla agentów, w tym Honcho
