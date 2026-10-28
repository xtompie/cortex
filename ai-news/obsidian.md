---
title: Obsidian i agenci AI
updated: 2026-10-28
tags: [obsidian, pkm, cli, agents, claude-code, plugins]
sources:
  - "[Obsidian Roadmap](https://obsidian.md/roadmap/) — 2026 — high"
  - "[Obsidian 1.13 Desktop (Public) — changelog](https://obsidian.md/changelog/2026-07-30-desktop-v1.13.4/) — 2026-07-30 — high"
  - "[Obsidian 1.13.0 Desktop (Early access) — changelog](https://obsidian.md/changelog/2026-05-28-desktop-v1.13.0/) — 2026-05-28 — high"
  - "[Obsidian (software) — Wikipedia](https://en.wikipedia.org/wiki/Obsidian_(software)) — 2026-10 — medium"
  - "[Claudian — Obsidian Plugin](https://community.obsidian.md/plugins/realclaudian) — 2026-10 — medium"
  - "[Copilot — Obsidian Plugin](https://community.obsidian.md/plugins/copilot) — 2026 — medium"
  - "[Agent Fleet — Obsidian Plugin](https://community.obsidian.md/plugins/agent-fleet) — 2026 — medium"
  - "[Obsidian Forum — Agent Client plugin](https://forum.obsidian.md/t/new-plugin-agent-client-bring-claude-code-codex-gemini-cli-inside-obsidian/108448) — 2025-11 — medium"
  - "[eugeniughelbur/obsidian-second-brain — GitHub](https://github.com/eugeniughelbur/obsidian-second-brain) — 2026-10 — medium"
---

# Obsidian i agenci AI

> Obsidian to aplikacja do notatek w zwykłych plikach Markdown. Dla agentów to idealny „mózg”: folder `.md`, który agent czyta i pisze, a człowiek przegląda z linkami i grafem. Od wersji 1.12 Obsidian ma oficjalny CLI do sterowania nim z terminala. Sam Obsidian nie ma wbudowanego agenta. Agentów dodają pluginy społeczności (Claudian, Copilot V4, Agent Client, Agent Fleet), które uruchamiają Claude Code, Codex czy OpenCode wewnątrz vaultu.

## Wersje

- **1.12**: Obsidian CLI do skryptów, automatyzacji i integracji z zewnętrznymi narzędziami.
- **1.13** (early access 2026-05-28, publicznie 2026-07-30 jako 1.13.4): nowy panel ustawień w osobnym oknie z wyszukiwaniem, pełnoekranowa przeglądarka obrazów, poprawka CLI dla flatpaka. Zmiana łamiąca zgodność: `--callout-color` przyjmuje kolor CSS zamiast tripletu RGB.
- **1.14.x**: według Wikipedii aktualna stabilna wersja to 1.14.4 z 2026-10-05. GitHub pokazuje już 1.14.5.
- Zmiany w CLI z changelogu, bez dokładnej wersji: szybsze połączenie bez wywoływania binarki Electrona, autouzupełnianie komend, `help <command>`, `daily:path`, rozdzielone `search` i `search:context`. Komendy działają domyślnie po cichu.

## Pluginy z agentami

- **Claudian**: uruchamia w vaulcie Claude Code, Codex, Grok Build, OpenCode, Pi, DeepSeek Harness i inne. Wersja 2.3.35, wymaga Obsidiana 1.13+. Według strony pluginu w połowie 2026 przekroczył 1,8 mln pobrań. Wsparcie OpenCode v1 kończy się 2026-10-30.
- **Copilot V4**: OpenCode, Claude Code i Codex w Obsidianie do researchu i pisania. Ma skille do Markdownu Obsidiana, Bases, Canvas i CLI.
- **Agent Client**: oparty na Agent Client Protocol (ACP) od Zed. Działa z każdym agentem zgodnym z ACP.
- **Agent Fleet**: autonomiczne agenty na harmonogramie, na Claude Code, Codex albo Pi. Integruje się ze Slackiem, Telegramem i Discordem.
- **obsidian-second-brain** (repo): pamięć dla agentów w vaulcie. Wersja 0.18 „Crew” z października 2026 daje wspólny dziennik dla Claude Code, Codex, Cursor i Grok Bot.

## Jak stosować

- Cortex jest zgodny z Obsidianem. Otwórz folder Cortex jako vault, a zobaczysz linki między stronami i graf stron.
- Plugin z agentem nie jest potrzebny, jeśli pracujesz w Claude Code w terminalu. Przydaje się, gdy chcesz pisać i pytać agenta z poziomu notatek.
- Nowe wersje śledź przez feed: `https://obsidian.md/changelog.xml`.

## Zobacz też
- [Pamięć dla agentów — Mem0, Letta, Zep/Graphiti, Honcho, Graphify](agent-memory.md) — inne podejścia do pamięci agentów
- [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md) — agenci, których pluginy uruchamiają w vaulcie
