---
title: Najpopularniejsze nowe repo AI (maj–październik 2026)
updated: 2026-10-28
tags: [github, trending, skills, agents, local-inference]
sources:
  - "[GitHub search: created:>2026-04-28, sort by stars](https://github.com/search?q=created%3A%3E2026-04-28&type=repositories&s=stars&o=desc) — 2026-10-28 — high"
  - "[DietrichGebert/ponytail — README](https://github.com/DietrichGebert/ponytail) — 2026-10-28 — high"
  - "[deepseek-ai/deepseek-harness — README](https://github.com/deepseek-ai/deepseek-harness) — 2026-10-28 — high"
---

# Najpopularniejsze nowe repo AI (maj–październik 2026)

> Repo AI z największą liczbą gwiazdek, założone po 2026-04-28. Stan z 2026-10-28. Widać trzy trendy. (1) Harnessy agentów od producentów modeli: DeepSeek Harness, Grok Build. (2) Skille, czyli jeden plik promptu, który zmienia zachowanie agenta: Ponytail, i-have-adhd, security-audit-skill, book-to-skill. (3) Lokalne uruchamianie dużych modeli MoE na zwykłym sprzęcie: colibri, ds4, Strata.

## Agenci i harnessy

- **deepseek-ai/deepseek-harness** (★265k, 2026-08-13): agent DeepSeek, „everything is a plugin”. Szczegóły w [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md).
- **xai-org/grok-build** (★28k, 2026-07-14): harness i TUI od xAI.
- **PrimeIntellect-ai/prime-agent** (★22k, 2026-05-08): samodoskonalący się agent RLM do długich zadań.
- **google-research/harness2** (★21k, 2026-10-06): bez opisu w repo.
- **yetone/magpie** (★25k, 2026-09-23): dowolny agent na dowolnym modelu z paska menu, np. Codex na DeepSeek albo Claude Code na Kimi.

## Skille i prompty

- **DietrichGebert/ponytail** (★179k, 2026-06-12): skill „najbardziej leniwego seniora w pokoju”. Najpierw czyta kod, który zmiana dotyka. Potem wybiera najmniejsze rozwiązanie. Nigdy nie tnie walidacji, bezpieczeństwa ani dostępności. Każda odpowiedź kończy się listą tego, czego nie sprawdził. Przykład z README: date picker w 10 liniach zamiast 335. Ma `/ponytail-review` i `/ponytail-audit`. Od wersji 5.3 w Claude Code pokazuje pasek z kosztem zadania. Instalacja: `/plugin marketplace add DietrichGebert/ponytail`.
- **ayghri/i-have-adhd** (★59k, 2026-05-13): skill, który każe agentowi podawać odpowiedź od razu, bez zakopywania jej w tekście.
- **cloudflare/security-audit-skill** (★52k, 2026-06-18): wielofazowy audyt bezpieczeństwa z niezależnie zweryfikowanymi wynikami w formacie maszynowym.
- **alibaba/open-code-review** (★49k, 2026-05-18): narzędzie do code review z deterministycznym pipeline'em i LLM.
- **virgiliojr94/book-to-skill** (★36k, 2026-05-01): zamienia PDF książki technicznej w skill do Claude Code.
- **microsoft/SkillOpt** (★19k, 2026-05-08): optymalizuje skille w języku naturalnym na podstawie przebiegów agenta.
- **wheresryan22/anatomy** (★22k, 2026-10-08): skill do interaktywnych ilustracji izometrycznych maszyn i systemów.
- **img2threejs/img2threejs** (★20k, 2026-07-15): odtwarza obiekt ze zdjęcia jako proceduralny model Three.js.

## Lokalne modele

- **JustVugg/colibri** (★45k, 2026-07-01): duże modele MoE na zwykłym sprzęcie. Czyste C, bez zależności, eksperci strumieniowani z dysku.
- **antirez/ds4** (★24k, 2026-05-06): silnik inferencji DeepSeek 4 Flash i Pro na Metal, CUDA i ROCm. Autor to twórca Redisa.
- **Niko1221/Strata** (★35k, 2026-09-24): Qwen3.8-Flash-Next na sprzęcie konsumenckim, instalacja jednym kliknięciem.
- **deepseek-ai/DeepInfer** (★24k, 2026-10-16): framework inferencji dla modeli DeepSeek na dużą skalę.

## Narzędzia dla agentów

- **firecrawl/anydoc** (★23k): Word, PowerPoint, Excel, PDF i EPUB do czystego Markdownu. Napisany w Ruście.
- **lexmount/moli** (★21k) i **browser-use/jev-ultrafast** (★24k): szybkie przeglądarki dla agentów.
- **baidu/Unlimited-OCR** (★29k): OCR długich dokumentów jednym przebiegiem.

## Uwaga

Sama liczba gwiazdek nie mówi o jakości. Niektóre repo z listy rosną podejrzanie szybko albo obchodzą zasady usług, np. `Ebony-Vinyl/dsh-our-free-model` obiecuje darmowe modele bez klucza API. Celowo ich tu nie polecam.

## Jak stosować

- Do pracy z Claude Code najciekawsze są skille: **ponytail** (mniej kodu, lepsze review) i **i-have-adhd** (odpowiedź na początku).
- Aby odświeżyć tę listę: `gh search repos "created:>RRRR-MM-DD" --sort stars --limit 40`, z datą sprzed 6 miesięcy.

## Zobacz też
- [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md) — główni agenci
- [Pamięć dla agentów — Mem0, Letta, Zep/Graphiti, Honcho, Graphify](agent-memory.md) — Graphify i inne narzędzia pamięci
