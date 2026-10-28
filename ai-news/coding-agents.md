---
title: Agenci kodujący — krajobraz (październik 2026)
updated: 2026-10-28
tags: [coding-agents, codex, opencode, cursor, antigravity, deepseek-harness, pi]
sources:
  - "[openai/codex — GitHub](https://github.com/openai/codex) — 2026-10-28 — high"
  - "[anomalyco/opencode — GitHub](https://github.com/anomalyco/opencode) — 2026-10-28 — high"
  - "[deepseek-ai/deepseek-harness — GitHub](https://github.com/deepseek-ai/deepseek-harness) — 2026-10-28 — high"
  - "[earendil-works/pi — GitHub](https://github.com/earendil-works/pi) — 2026-10-28 — high"
  - "[The Register — Bye-bye, Gemini CLI](https://www.theregister.com/ai-ml/2026/05/20/bye-bye-gemini-cli-google-nudges-devs-toward-antigravity/5243605) — 2026-05-20 — high"
  - "[Virtualization Review — Google Moves Gemini CLI Into Antigravity CLI](https://virtualizationreview.com/articles/2026/05/19/google-moves-gemini-cli-into-antigravity-cli-as-agent-platform-expands.aspx) — 2026-05-19 — medium"
  - "[Pinggy — Top 5 CLI coding agents in 2026](https://pinggy.io/blog/top_cli_based_ai_coding_agents/) — 2026-10 — low"
  - "[Morph — Best AI Coding Agents (October 2026)](https://www.morphllm.com/best-ai-coding-agents-2026) — 2026-10 — low"
  - "[stablyai/orca — GitHub](https://github.com/stablyai/orca) — 2026-10-28 — high"
  - "[farion1231/cc-switch — GitHub](https://github.com/farion1231/cc-switch) — 2026-10-28 — high"
  - "[openai/codex-plugin-cc — GitHub](https://github.com/openai/codex-plugin-cc) — 2026-10-28 — high"
---

# Agenci kodujący — krajobraz (październik 2026)

> Rynek agentów kodujących dzieli się na trzy grupy. Pierwsza to agenci producentów modeli: Claude Code, Codex, Antigravity CLI, DeepSeek Harness i Grok Build. Druga to otwarte harnessy na dowolny model: OpenCode, Pi, Cline i Aider. Trzecia to edytory z agentami, np. Cursor. Do tego dochodzi nowa warstwa: narzędzia do sterowania wieloma agentami naraz (Orca, cc-switch). Wspólny trend: równoległe agenty w osobnych git worktree.

## Agenci producentów modeli

| Agent | Stan na 2026-10-28 | Licencja | Gwiazdki |
|---|---|---|---|
| **Claude Code** (Anthropic) | osobna strona | — | — |
| **Codex CLI** (OpenAI) | `rust-v0.165.0` z 2026-10-27, alfy 0.166 codziennie | Apache-2.0 | ★131k |
| **Antigravity CLI** (Google) | następca Gemini CLI, binarka `agy`, Go | zamknięty kod (sporne) | — |
| **DeepSeek Harness** (`dsh`) | developer preview, `dsh-v0.2.2-alpha.2` z 2026-10-28 | MIT | ★265k |
| **Grok Build** (xAI) | harness + TUI, repo od 2026-07-14 | Apache-2.0 | ★28k |

- **Gemini CLI** został wycofany. Google ogłosił to na I/O 19 maja 2026. Od 18 czerwca 2026 Gemini CLI nie obsługuje użytkowników AI Pro, Ultra i darmowych. Zostaje tylko dla firm i kluczy API. Repo `google-gemini/gemini-cli` (★109k) nadal wydaje wersje, np. `v0.66.0` z 2026-10-27.
- **Antigravity 2.0** to aplikacja desktop do zarządzania agentami, CLI i SDK. Twórcy narzekają, że CLI nie jest otwarte. Jedno źródło twierdzi, że ma licencję Apache 2.0, ale samo oznacza to jako niesprawdzone.
- **DeepSeek Harness** powstał 2026-08-13 i jest najszybciej rosnącym repo AI tego roku. Architektura „everything is a plugin” na frameworku Cordis. Uruchomienie: `npx @deepseek-ai/dsh web`. Autorzy uprzedzają, że będą zmiany łamiące zgodność.

## Otwarte harnessy (dowolny model)

- **OpenCode** (`anomalyco/opencode`, ★223k, MIT): najpopularniejszy otwarty agent. 2026-10-27 wyszła wersja `v2.2.0`, a linia 1.x dostaje dalej poprawki (`v1.19.5`). Obsługuje 75+ dostawców modeli. Jakość zależy od wybranego modelu.
- **Pi** (`earendil-works/pi`, ★119k): toolkit agenta: wspólne API do LLM, pętla agenta, TUI i CLI. Na nim działa część innych narzędzi, np. plugin Agent Fleet do Obsidiana.
- **Cline** (★71k): agent jako SDK, rozszerzenie IDE albo CLI. Mocny w trybie „bring your own key”.
- **Aider** (★50k): klasyczny pair programmer w terminalu.

## Edytory z agentami

- **Cursor 3**: IDE z agentami w tle w chmurze i z równoległymi agentami w worktree.
  > **Status: Disputed** — Jeden blog (Pinggy) podaje, że SpaceX przejął Cursor za 60 mld USD 14 sierpnia 2026 i że Cursor dodał modele Grok. Nie znalazłem drugiego źródła. Źródła różnią się też w cennikach (Pro 20 USD; wyższe progi 40/60/200 USD).

## Warstwa nad agentami

- **Orca** (`stablyai/orca`, ★109k, od 2026-03-17): miejsce do pracy z flotą agentów (Claude Code, Grok Bot i inne), każdy w swoim worktree.
- **cc-switch** (★150k): desktopowa aplikacja do przełączania konfiguracji Claude Code, Codex, OpenCode, OpenClaw, Grok Build i Hermes.
- **codex-plugin-cc** (OpenAI, ★35k, od 2026-03-30): wywołanie Codex z Claude Code, np. do review albo oddania zadania.

## Benchmarki

Według blogów porównawczych na Terminal-Bench 4.0 (2026-10-06) prowadzi Claude Code z Opus 5.5 (64.8%), przed Codex z GPT-6.1 Sol (58.2%). To dane z blogów, nie z oficjalnej tabeli. Traktuj je jako orientacyjne.

## Jak stosować

- Pracujesz w Claude Code i chcesz drugiej opinii przy review → `codex-plugin-cc`.
- Chcesz otwartej alternatywy na tańszym modelu → OpenCode albo Pi z modelem DeepSeek/Kimi/Qwen.
- Puszczasz kilka agentów równolegle → Orca albo własne git worktree.
- Używałeś Gemini CLI na prywatnym koncie → przejdź na Antigravity CLI albo na OpenCode z kluczem Gemini API.
- Nowości śledź przez feedy wydań: `https://github.com/<owner>/<repo>/releases.atom`.

## Zobacz też
- [Hermes Agent (Nous Research)](hermes-agent.md) — agent osobisty z pamięcią, nie tylko do kodu
- [Spec-driven development — OpenSpec, Spec Kit, BMAD, Open Mercato](spec-driven-tools.md) — procesy, które te agenty wykonują
- [Najpopularniejsze nowe repo AI (maj–październik 2026)](trending-repos-2026.md) — skille i dodatki do agentów, które zyskały popularność
