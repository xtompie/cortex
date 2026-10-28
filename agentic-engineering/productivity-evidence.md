---
title: Dowody na produktywność z agentami kodującymi
updated: 2026-10-28
tags: [productivity, metr, dora, research, pull-requests]
sources:
  - "[Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity (METR)](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/) — 2025-07-10 — high"
  - "[METR uplift update](https://metr.org/blog/2026-02-24-uplift-update/) — 2026-02-24 — high"
  - "[Announcing the 2025 DORA report (Google Cloud)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report) — 2025-09 — high"
  - "[Agentic PRs vs human PRs (ACM, MSR '26)](https://dl.acm.org/doi/10.1145/3798166) — 2026 — high"
  - "[Pinna i in. — agent PRs (arXiv 2602.08915)](https://arxiv.org/html/2602.08915v2) — 2026 — high"
  - "[How Coding Agents Fail Their Users (Tang i in., arXiv 2605.29442)](https://arxiv.org/abs/2605.29442) — 2026-08-31 — high"
---

# Dowody na produktywność z agentami kodującymi

> Twardych danych jest mało i są niepewne. Jedyne badanie RCT (METR 2025) pokazało spowolnienie o 19%, choć programiści czuli przyspieszenie. Kontynuacja z 2026 roku wskazuje raczej przyspieszenie, ale METR sam nazywa te dane niewiarygodnymi. DORA widzi wzrost przepustowości i spadek stabilności dostaw tam, gdzie brakuje testów i szybkiej informacji zwrotnej.

## METR — RCT 2025

- 16 doświadczonych programistów, 246 zadań w ich własnych repo. Narzędzia: „Cursor Pro with Claude 3.5/3.7 Sonnet”.
- Z AI „they take 19% longer”.
- Przed badaniem oczekiwali przyspieszenia o 24%. Po badaniu uważali, że AI przyspieszyło ich o 20%.
- Strona jest teraz oznaczona: „These results are out of date.”

## METR — aktualizacja 2026-02-24

- Powracający uczestnicy: „-18% with a confidence interval between -38% and +9%”. Nowi: „-4%, … -15% and +9%”. Minus oznacza szybciej. Oba przedziały obejmują zero.
- METR sam ostrzega przed danymi: programiści mocno korzystający z AI odmawiali udziału, stawka spadła ze $150 do $50 za godzinę, pomiar czasu przy kilku agentach naraz jest niepewny, 30–50% zadań uczestnicy zatrzymali dla siebie.

> **Status: Disputed** — RCT 2025: spowolnienie o 19%. Aktualizacja 2026: raczej przyspieszenie, ale wynik nieistotny statystycznie i z zastrzeżeniami samego METR.

## DORA 2025

- Ok. 5 000 respondentów. Używa AI 90% (+14%). Mediana ok. 2 godziny dziennie.
- AI to „amplifier”. Ma dodatni związek z przepustowością i „a negative relationship with software delivery stability”, gdy brakuje dobrych testów, kontroli wersji i szybkiej informacji zwrotnej.
- Ponad 80% deklaruje wzrost produktywności. To samoocena.

## PR od agentów (MSR '26)

- Badanie ACM: zaakceptowano 83,8% PR od agentów i 91,0% PR od ludzi (po 567).
- Pinna i in. (7 156 PR): dokumentacja 82,1%, funkcje 66,1% akceptacji. Akceptacja to „a weak proxy for quality”.
- Tang i in. (20 574 sesje): „91.49% of visible resolutions still require explicit user correction.”

## Jak stosować

1. Nie ufaj własnemu poczuciu przyspieszenia. W METR uczestnicy czuli przyspieszenie o 20%, a pomiar pokazał spowolnienie o 19%.
2. Mierz na swoich zadaniach: czas do merge, liczbę poprawek po review, incydenty.
3. Inwestuj w testy i szybkie CI przed zwiększaniem udziału agentów. DORA łączy spadek stabilności z ich brakiem.

## Zobacz też
- [Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md) — weryfikacja jako odpowiedź na spadek stabilności
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — proces z kontrolą jakości
