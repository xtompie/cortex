---
title: Krajobraz modeli LLM (stan na 2026-10-28)
updated: 2026-10-28
tags: [models, llm, benchmarks, leaderboards, openai, google, anthropic, xai, meta]
sources:
  - "[Announcing Artificial Analysis Intelligence Index v5](https://artificialanalysis.ai/articles/artificial-analysis-intelligence-index-v5) — 2026-10-27 — high"
  - "[LLM Gateway — LLMs Released in 2026](https://llmgateway.io/timeline/2026) — 2026-10-23 — medium"
  - "[9to5Google — Gemini 4 Carbon announcement](https://9to5google.com/2026/10/28/gemini-4-carbon-announcement/) — 2026-10-28 — medium"
  - "[TechCrunch — OpenAI launches GPT-6 Sol and Luna](https://techcrunch.com/2026/09/22/openai-launches-gpt-6-sol-and-luna/) — 2026-09-22 — medium"
  - "[CNBC — OpenAI announces rollout of GPT-6 Astra](https://www.cnbc.com/2026/09/03/open-ai-astra-gpt-6-cyber.html) — 2026-09-03 — medium"
  - "[9to5Mac — GPT-6 in ChatGPT and Intelligent UI](https://9to5mac.com/2026/10/07/openai-brings-gpt-6-to-chatgpt-and-debuts-intelligent-ui/) — 2026-10-07 — medium"
  - "[Manifold — #1 model on Arena text leaderboard on Oct 31, 2026](https://manifold.markets/Terminator2/which-company-will-have-the-1-model) — 2026-10 — low"
  - "[versusapps — LMArena Leaderboard October 2026](https://www.versusapps.com/blog/lmarena-leaderboard-september-2026) — 2026-10-20 — low"
  - "[morphllm — SWE-bench Pro Leaderboard (October 2026)](https://www.morphllm.com/swe-bench-pro) — 2026-10 — low"
  - "[morphllm — Best AI Coding Agents (October 2026)](https://www.morphllm.com/best-ai-coding-agents-2026) — 2026-10 — low"
---

# Krajobraz modeli LLM (stan na 2026-10-28)

> Czołówkę trzymają trzy firmy: Anthropic, OpenAI i Google. Ogólne rankingi zmieniają lidera co kilka tygodni. W kodowaniu najczęściej prowadzi Claude Opus 5.5. W Arena (głosy ludzi) prowadzi Gemini 4 Argon. Na indeksie Artificial Analysis v5 od 28 października prowadzi Gemini 4 Carbon, ale ten model mają na razie tylko wybrani partnerzy od cyberbezpieczeństwa. Najlepsze otwarte modele są z Chin (Kimi, GLM, DeepSeek, Qwen) i z Meta.

## Kto prowadzi gdzie

| Ranking | Lider | Uwagi |
|---|---|---|
| Artificial Analysis Intelligence Index v5 | Gemini 4 Carbon — 59 (według Google i AA, 2026-10-28) | Przy starcie v5 (2026-10-27): Claude Opus 5.5 (max) 58, GPT-6 Astra (max) 57, GPT-6.1 Sol (max) 55. Według AA „Anthropic and OpenAI hold the top five models” przed wejściem Carbon. |
| AA Coding Agent Index | Claude Opus 5.5 | Gemini 4 Carbon jest „second only to Claude Opus 5.5”. |
| FrontierCode 2.0 (kod, w AA v5) | Claude Opus 5.5 (max) — 46% | GPT-6 Astra, GPT-6.1 Terra, Claude Sonnet 5.5 — po 42%. |
| Arena text (dawniej LMArena, teraz arena.ai) | Gemini 4 Argon (High) — 1532 bez style control | Dalej cztery modele Claude (Opus 5.5, Fable 5.1, Opus 5). Najlepszy model OpenAI był 2 października dopiero na #20. Źródła wtórne, sprawdzaj na arena.ai. |
| Terminal-Bench 4.0 (agent + model) | Claude Code + Opus 5.5 — 64.8% | Codex + GPT-6 Astra — 58.2%. Dane z agregatora. |
| SWE-bench Pro | Claude Opus 5.5 — 89.9% (wynik podany przez Anthropic) | Standaryzowany zestaw Scale SEAL daje inną kolejność i dużo niższe liczby. Wyników vendorów nie porównuj z tablicą Scale. |

> **Status: Disputed** — SWE-bench Pro: wyniki zgłaszane przez producentów (62.5%–89.9%) i niezależna tablica Scale SEAL (lider Muse Spark 1.1, 61.5%) się nie zgadzają. Według agregatora morphllm audyt OpenAI z lipca 2026 ocenił, że około 30% zadań w publicznym zbiorze jest wadliwych.

## Firmy — co wyszło w ostatnich ~6 miesiącach

**Anthropic.** Claude Opus 4.8 (05-28), Claude Fable 5 (06-09), Sonnet 5 (06-30), Opus 5 (07-24), Fable 5.1 (09-01), Opus 5.5 (09-22), Sonnet 5.5 (09-28), Haiku 5.5 (10-07). Szczegóły w osobnej stronie o Anthropic i Claude Code.

**OpenAI.** GPT-5.6 Sol/Terra/Luna (07-09). GPT-6 Astra (09-03): najpierw tylko dla partnerów z programu cyberbezpieczeństwa, bo według OpenAI to pierwszy model na poziomie „Critical” w ich wewnętrznej skali zagrożeń cyber. GPT-6 Sol i Luna (09-22): według OpenAI o połowę tańsze od serii 5.6. GPT-6.1 Sol (09-29): według OpenAI kodowanie blisko Astry za jedną piątą ceny. GPT-6.1 Terra (10-15). W ChatGPT od 7–8 października GPT-6 Sol dla płatnych i Luna dla darmowych, razem z „Intelligent UI”, czyli interaktywnymi widżetami w odpowiedziach. Nazewnictwo: Astra to największy model, Sol średni, Terra i Luna mniejsze i szybsze.

**Google.** Gemini 3.5/3.6/3.7/3.8 Flash (maj–wrzesień), Gemini 4 Argon (ogłoszony 09-30, szersze udostępnienie 10-13), Gemini 4 Carbon (10-28). Carbon jest na start tylko dla wybranych obrońców cyber, publicznej daty nie ma. Cena wejściowa API: $2 za milion tokenów wejścia i $10 za milion wyjścia, później $4/$20 (według 9to5Google). Grafika: Nano Banana 2.1 (10-06).

**xAI.** Grok 4.5 (07-08), 4.6 (08-06), 4.7 (09-21), do tego modele głosowe i wideo (Grok Voice 3.0, Grok Imagine Video 1.5). W Arena najlepszy model xAI był 2 października na #36.

**Meta.** Rodzina Muse: Muse Spark 1.1–1.3 (lipiec–wrzesień), Muse Wonder 1.0 (10-12, zamknięty, najmocniejszy), Muse Spark Open (10-15, otwarte wagi). Patrz [Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)](open-weight-models.md).

**Chiny i inni.** Kimi K3 (07-16) i K3.1 Pro (10-23) od Moonshot, GLM-5.2/5.3 od Z.AI (Zhipu), DeepSeek V4 i V4.1 Flash, Qwen3.7/3.8 od Alibaby, MiniMax M3, Mistral Large 4 (10-06), NVIDIA Nemotron 3.5. Patrz [Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)](open-weight-models.md).

## Trendy

- **Rytm wydań.** LLM Gateway naliczył w październiku 2026 do 23. dnia 20 nowych modeli od 16 dostawców. Duże firmy wydają kolejne wersje co kilka tygodni.
- **Wydania etapowe z powodu cyberbezpieczeństwa.** GPT-6 Astra i Gemini 4 Carbon trafiły najpierw do partnerów od cyberobrony, a dopiero potem dalej. Według CNBC OpenAI opóźniło wydanie po incydentach z agentami w lipcu i sierpniu 2026.
- **Rozumowanie kosztuje tokeny.** W AA v5 mediana tokenów wyjścia na zadanie wzrosła z 35k (v4.3) do 59k. Ten sam model daje bardzo różny wynik zależnie od poziomu „effort”: Claude Opus 5.5 ma 35 punktów na niskim i 58 na maksymalnym.
- **Cena za zadanie, nie za token.** Koszt jednego zadania z indeksu AA: Claude Opus 5.5 (max) $10.04, GPT-6 Astra (max) $6.24, GPT-6.1 Sol (max) $1.27. Wśród 10 najlepszych najtańszy był GPT-6.1 Terra (max), $0.96, a najdroższy Claude Fable 5.1 (max), $13.04.
- **Kontekst 1M tokenów** jest standardem u dużych otwartych modeli (DeepSeek V4, GLM-5.2, Kimi K3, Muse Spark Open).
- **Rankingi się rozjeżdżają.** AA v5 opiera 60% wagi na prywatnych testach, żeby ograniczyć uczenie się pod benchmark. Arena mierzy preferencje ludzi. Vendorzy podają własne liczby. Wybieraj ranking pasujący do zadania.

## Ostatnie zmiany

- 2026-10-28 — Google ogłasza Gemini 4 Carbon. Według Google i AA ma 59 punktów i jest #1 w AA v5. Dostęp na razie ograniczony.
- 2026-10-27 — Artificial Analysis wydaje Intelligence Index v5: prywatne testy, nowe FrontierCode 2.0 i Terminal-Bench-Science.
- 2026-10-23 — Moonshot wydaje Kimi K3.1 Pro (API, wagi jeszcze niewydane).
- 2026-10-15 — Meta udostępnia wagi Muse Spark Open. OpenAI wydaje GPT-6.1 Terra.
- 2026-10-07 — Anthropic wydaje Claude Haiku 5.5. GPT-6 trafia do ChatGPT.
- 2026-10-06 — Mistral Large 4 w podglądzie API.
- 2026-09-22 — OpenAI GPT-6 Sol i Luna. Anthropic Claude Opus 5.5.
- 2026-09-03 — OpenAI GPT-6 Astra w ograniczonym podglądzie.

## Jak stosować

Stan na 2026-10-28. Sprawdzaj ponownie co kilka tygodni.

- **Kodowanie z agentem (Claude Code, Codex):** Claude Opus 5.5 to najmocniejszy wybór według kilku niezależnych tablic. Claude Sonnet 5.5 jest blisko i tańszy. Po stronie OpenAI GPT-6.1 Sol daje kodowanie blisko Astry za ułamek ceny.
- **Najlepsza cena za jakość:** GPT-6.1 Sol i GPT-6.1 Terra mają najniższy koszt zadania w czołówce AA.
- **Rozmowa i ogólne odpowiedzi:** w Arena prowadzi Gemini 4 Argon.
- **Szybko i tanio w agencie:** Claude Haiku 5.5. Według AA ma 36 punktów (max) i bije najlepsze modele z publicznie wydanymi wagami.
- **Własny serwer albo dane, które nie mogą wyjść:** patrz [Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)](open-weight-models.md).
- **Jak czytać rankingi:** liczby od producenta traktuj jako marketing, dopóki nie potwierdzi ich AA, Arena, Scale SEAL albo Vals AI. Porównuj wyniki z tej samej tablicy i przy tym samym poziomie effort.

## Zobacz też
- [Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)](open-weight-models.md) — otwarte modele i co uruchomić lokalnie
