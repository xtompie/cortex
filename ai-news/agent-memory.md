---
title: Pamięć dla agentów — Mem0, Letta, Zep/Graphiti, Honcho, Graphify
updated: 2026-10-28
tags: [memory, agents, mem0, letta, zep, graphiti, honcho, graphify, knowledge-graph]
sources:
  - "[Braintrust — Best AI agent memory tools in 2026](https://www.braintrust.dev/articles/best-ai-agent-memory-tools-2026) — 2026 — medium"
  - "[Atlan — Best AI Agent Memory Frameworks in 2026](https://atlan.com/know/best-ai-agent-memory-frameworks-2026/) — 2026 — medium"
  - "[The Tool Nerd — Your Coding Agent Has Amnesia](https://www.thetoolnerd.com/p/your-coding-agent-has-amnesia-the) — 2026 — medium"
  - "[mem0ai/mem0 — GitHub](https://github.com/mem0ai/mem0) — 2026-10-28 — high"
  - "[letta-ai/letta — GitHub](https://github.com/letta-ai/letta) — 2026-10-28 — high"
  - "[plastic-labs/honcho — GitHub](https://github.com/plastic-labs/honcho) — 2026-10-28 — high"
  - "[Graphify-Labs/graphify — GitHub](https://github.com/Graphify-Labs/graphify) — 2026-10-28 — high"
  - "[rohitg00/agentmemory — GitHub](https://github.com/rohitg00/agentmemory) — 2026-10-28 — medium"
---

# Pamięć dla agentów — Mem0, Letta, Zep/Graphiti, Honcho, Graphify

> Agenci sesyjni zapominają wszystko po zamknięciu sesji. Są trzy podejścia, żeby to naprawić. (1) Biblioteki pamięci, które wyciągają fakty z rozmów: Mem0, Letta, Zep/Graphiti, Honcho. (2) Grafy wiedzy z kodu i dokumentów, np. Graphify. (3) Pamięć w zwykłych plikach Markdown, np. LLM Wiki, Obsidian albo Cortex. Mem0 to domyślny wybór do pamięci o użytkowniku. Graphify to najszybciej rosnące narzędzie do pamięci o kodzie.

## Biblioteki pamięci

| Narzędzie | Podejście | Licencja | Gwiazdki (2026-10-28) |
|---|---|---|---|
| **Mem0** | fakty i preferencje z rozmów → baza wektorowa, opcjonalnie graf | Apache-2.0 | ★68k |
| **Letta** (dawniej MemGPT) | agent sam edytuje swoje bloki pamięci narzędziami | Apache-2.0 | ★25k |
| **Zep / Graphiti** | pamięć czasowa: fakty zmieniające się w czasie, graf | Graphiti Apache-2.0, Zep komercyjny | Graphiti ★32k (wg Braintrust) |
| **Honcho** | modelowanie użytkownika w długim okresie; używa go Hermes Agent | AGPL-3.0 | ★7.8k |

- Letta: według jednego źródła zmiana z marca 2026 wycofuje serwerowe narzędzia pamięci, szablony, tożsamości i integracje MCP. Sprawdź przed wyborem.
- Zep podobno wycofał self-hosted Community Edition.
- Inne nazwy w zestawieniach 2026: Cognee (graf + serwer MCP), Supermemory, LangMem, Hindsight, TencentDB Agent Memory, Cloudflare Agent Memory.

## Pamięć o kodzie

- **Graphify** (★138k, od 2026-04-03): zamienia repo razem z dokumentacją, schematami SQL, konfiguracją i PDF-ami w graf wiedzy, o który można pytać. Ma komendę `/graphify` dla agentów.
- **agentmemory** (`rohitg00/agentmemory`, ★30k): trwała pamięć dla agentów kodujących, oparta na benchmarkach.

## Pamięć w plikach Markdown

To nurt LLM Wiki Karpathy'ego z kwietnia 2026: agent prowadzi wiki w `.md` zamiast bazy wektorowej. Implementacje to m.in. `nvk/llm-wiki`, `AgriciDaniel/claude-obsidian` i Cortex. Zaleta: wszystko jest czytelne, w gicie i niezależne od dostawcy. Wada: przy setkach stron potrzebna jest wyszukiwarka.

## Jak stosować

- Budujesz aplikację, która ma pamiętać użytkownika → Mem0, a gdy fakty zmieniają się w czasie → Graphiti.
- Agent kodujący gubi się w dużym repo → Graphify.
- Wiedza osobista i notatki → Markdown wiki: Cortex albo Obsidian.

## Zobacz też
- [Hermes Agent (Nous Research)](hermes-agent.md) — agent z wbudowaną pamięcią (Honcho)
- [Obsidian i agenci AI](obsidian.md) — pamięć w vaulcie Obsidiana
