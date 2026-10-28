---
title: Context engineering dla agentów kodujących
updated: 2026-10-28
tags: [context-engineering, context-rot, agents, claude-code, codex]
sources:
  - "[Effective context engineering for AI agents (Anthropic)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — 2025-09-29 — high"
  - "[Context Rot (Chroma; Hong, Troynikov, Huber)](https://www.trychroma.com/research/context-rot) — 2025-07-14 — high"
  - "[How Long Contexts Fail (Drew Breunig)](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html) — 2025-06-22 — medium"
  - "[Context Engineering for Coding Agents (Birgitta Böckeler, martinfowler.com)](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) — 2026-02-05 — high"
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Advanced Context Engineering for Coding Agents (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md) — unknown — medium"
  - "[Agentic Engineering Patterns — Subagents (Simon Willison)](https://simonwillison.net/guides/agentic-engineering-patterns/subagents/) — unknown — high"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
---

# Context engineering dla agentów kodujących

> Context engineering to dobór tego, co model widzi w danej chwili. Jakość odpowiedzi spada, gdy kontekst rośnie, długo przed limitem okna. Dlatego trzymasz kontekst krótki i na temat: czyścisz go między zadaniami, ciężką pracę oddajesz subagentom, a wiedzę trwałą zapisujesz w plikach. Spór dotyczy tylko tego, jak agresywnie to robić przy oknach 1M tokenów.

## Definicja

- Anthropic: „the set of strategies for curating and maintaining the optimal set of tokens” w czasie inferencji. Model ma „attention budget”. Transformer tworzy „n² pairwise relationships for n tokens”.
- Böckeler cytuje Bharaniego Subramaniama: „Context engineering is curating what the model sees so that you get a better result.”

## Context rot — dlaczego długi kontekst szkodzi

- Anthropic: gdy kontekst rośnie, „the model's ability to accurately recall information from that context decreases”.
- Chroma przetestowała 18 modeli (m.in. GPT-4.1, Claude 4, Gemini 2.5, Qwen3): „Across all experiments, model performance consistently degrades with increasing input length.”
  - Jeden dystraktor obniża wynik poniżej bazy. Cztery obniżają go jeszcze bardziej.
  - LongMemEval: pełny prompt ok. 113k tokenów kontra skupiony ok. 300 tokenów. Skupiony wygrywa u wszystkich modeli.
  - Chroma nie wyjaśnia mechanizmu: „We also do not explain the mechanisms behind this performance degradation.”
- Willison: okna „generally top out at around 1,000,000, and benchmarks frequently report better quality results below 200,000.”

## Cztery sposoby, w jakie kontekst psuje wynik (Breunig)

- **Poisoning** — błąd albo halucynacja trafia do kontekstu i model ciągle się na nią powołuje.
- **Distraction** — kontekst tak długi, że model powtarza wcześniejsze akcje zamiast myśleć. Agent Gemini grający w Pokémon zaczął to robić powyżej 100k tokenów.
- **Confusion** — zbędne treści wpływają na odpowiedź. Skwantowana Llama 3.1 8b przegrała z 46 narzędziami, a wygrała z 19.
- **Clash** — sprzeczne informacje w kontekście. Prompt podzielony na kawałki dał średni spadek 39%, o3 spadł z 98.1 do 64.1.

HumanLayer układa szkodliwość tak: najgorsza jest zła informacja, potem brak informacji, na końcu szum.

## Rodzaje kontekstu (Böckeler)

- **Instrukcje** — wielokrotne prompty i reguły (CLAUDE.md, AGENTS.md, rules).
- **Interfejsy kontekstu** — narzędzia, MCP, skille.
- **Pliki w workspace** — kod i dokumenty, które agent czyta.

Kto decyduje o załadowaniu:
- model — skille ([Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md)),
- człowiek — slash commands,
- oprogramowanie agenta — hooki.

Böckeler: „An agent's effectiveness goes down when it gets too much context.” Pliki reguł buduj stopniowo.

## Techniki

- **Just-in-time retrieval** — agent szuka plików przez glob i grep, zamiast ładować wszystko na start (Anthropic).
- **Structured note-taking** — agent zapisuje notatki poza oknem kontekstu i czyta je później (Anthropic).
- **Czyszczenie wyników narzędzi** — „One of the safest lightest touch forms of compaction” (Anthropic).
- **Izolacja w subagentach** — ciężkie czytanie w osobnym oknie, z powrotem wraca streszczenie ([Subagenty i praca wieloagentowa](subagents.md)).
- **Celowa kompakcja** — HumanLayer streszcza postęp do plików research i plan. Trzyma zużycie kontekstu w przedziale 40–60%. To heurystyka jednego zespołu, bez pomiarów.
- **Krótkie pliki instrukcji** — Claude Code: „every line in it takes a little of Claude's attention on *every* task” ([AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md)).

## Spór: czy rozmiar kontekstu jeszcze ma znaczenie

- Obecna strona best practices Claude Code wpisuje „The context window is your main constraint, manage it aggressively” na listę przestarzałych rad. Przy 1M tokenów i automatycznej kompakcji „running out is rare”. Ta sama strona dalej każe robić `/clear`, bo „a focused context gets you better answers”.
- Chroma, Breunig i Willison pokazują spadek jakości dużo wcześniej niż przy końcu okna. HumanLayer celuje w 40–60%.
- Wniosek: brak miejsca to dziś rzadki problem. Spadek jakości przy długim kontekście nadal jest realny.

## Jak stosować

1. Jedno zadanie, jeden kontekst. `/clear` między niezwiązanymi zadaniami (Claude Code). Codex: „Keep one chat per coherent unit of work”.
2. Rób research i czytanie wielu plików w subagencie. Do głównej sesji ma wrócić streszczenie.
3. Wiedzę, która ma przetrwać sesję, zapisuj w plikach: spec, plan, plik postępu ([Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy](session-management.md)).
4. Gdy agent się zapętla albo powtarza błąd, zacznij od czystego kontekstu z lepszym promptem. Nie poprawiaj go trzeci raz w tym samym wątku.
5. Podejrzyj, co siedzi w kontekście: `/context` w Claude Code.
6. Nie wklejaj długich logów i całych plików, jeśli wystarczy ścieżka i numer linii.

## Zobacz też
- [Subagenty i praca wieloagentowa](subagents.md) — izolacja kontekstu i jej koszt
- [Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy](session-management.md) — kiedy nowa sesja, `/clear`, kompakcja, pliki przekazania
- [AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md) — kontekst ładowany zawsze
- [Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md) — kontekst ładowany na żądanie
