---
title: Anthropic — modele, produkty i limity (maj–październik 2026)
updated: 2026-10-28
tags: [anthropic, claude, models, pricing, limits, claude-design]
sources:
  - "[anthropics/claude-code CHANGELOG.md](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) — 2026-10-27 — high"
  - "[Introducing Claude Sonnet 5.5 (Anthropic)](https://www.anthropic.com/claude-sonnet-5-5) — 2026-09-28 — high"
  - "[Claude Fable (Anthropic)](https://www.anthropic.com/claude/fable) — unknown — high"
  - "[Higher usage limits and a SpaceX compute deal (Anthropic)](https://www.anthropic.com/news/higher-limits-spacex) — 2026-05-06 — high"
  - "[Move from standalone Claude Design to Claude (support.claude.com)](https://support.claude.com/en/articles/17440474-move-from-standalone-claude-design-to-claude) — 2026-10-08 — high"
  - "[Claude on X: Haiku 5.5](https://x.com/claudeai/status/2107894039626277339) — 2026-10-07 — high"
  - "[Claude on X: Sonnet 5 pricing permanent](https://x.com/claudeai/status/2086891169217122586) — 2026-08 — high"
  - "[TechCrunch: Anthropic launches Opus 5](https://techcrunch.com/2026/07/24/anthropic-launches-opus-5/) — 2026-07-24 — high"
  - "[TechCrunch: Claude Sonnet 5](https://techcrunch.com/2026/06/30/anthropic-launches-claude-sonnet-5-as-a-cheaper-way-to-run-agents/) — 2026-06-30 — high"
  - "[CNBC: Claude Fable 5](https://www.cnbc.com/2026/06/09/anthropic-mythos-claude-fable-5.html) — 2026-06-09 — high"
  - "[InfoQ: Anthropic Releases and Temporarily Suspends Claude Fable 5](https://www.infoq.com/news/2026/06/claude-5-release/) — 2026-06 — medium"
  - "[Fortune: Claude Opus 5](https://fortune.com/2026/07/24/anthropic-debuts-claude-opus-5-with-feature-that-lets-users-toggle-between-cost-and-capability/) — 2026-07-24 — medium"
  - "[VentureBeat: Claude Haiku 5.5](https://venturebeat.com/technology/anthropic-launches-claude-haiku-5-5-with-90-api-price-reduction-matching-gpt-6-luna) — 2026-10-07 — medium"
  - "[9to5Mac: Haiku 5.5](https://9to5mac.com/2026/10/07/anthropic-upgrades-claude-with-new-haiku-5-5-model-details-here/) — 2026-10-07 — medium"
  - "[Unite.AI: Claude Dashboards and Motion](https://www.unite.ai/anthropic-launches-claude-dashboards-and-motion-takes-docs-out-of-beta/) — 2026-10-08 — medium"
  - "[explainx.ai: Claude usage limits 2026 timeline](https://www.explainx.ai/blog/claude-usage-limits-2026-timeline-explained) — 2026 — low"
---

# Anthropic — modele, produkty i limity (maj–październik 2026)

> Od maja do października 2026 Anthropic wydał dwie generacje modeli: Claude 5 (czerwiec–lipiec) i Claude 5.5 (wrzesień–październik). Obecny zestaw: **Opus 5.5** do złożonej pracy, **Sonnet 5.5** do codziennych zadań, **Haiku 5.5** do szybkich i tanich zadań oraz **Fable 5.1** jako najmocniejszy model publiczny (wersja Mythos). Każda nowa generacja jest tańsza od poprzedniej. Do tego Claude Design, Docs i Slides weszły do zwykłej rozmowy, a limity w Claude Code kilka razy wzrosły.

## Obecne modele (stan na 2026-10-28)

| Model | ID | Wydany | Cena wejście/wyjście za Mtok | Do czego |
|---|---|---|---|---|
| Claude Fable 5.1 | `claude-fable-5-1` | 2026-09-01 | $10 / $50 | najmocniejszy publiczny model, wersja Mythos |
| Claude Opus 5.5 | `claude-opus-5-5` | 2026-09-22 | $4 / $20 | złożona praca wymagająca osądu |
| Claude Sonnet 5.5 | `claude-sonnet-5-5` | 2026-09-28 | $2 / $10 | codzienne, dobrze określone zadania, poprawki błędów, dokumenty |
| Claude Haiku 5.5 | `claude-haiku-5-5` | 2026-10-07 | $0.10 / $0.50 (do 100K tokenów promptu) | dużo szybkich zadań, subagenci, klasyfikacja, obsługa przeglądarki |

Wszystkie cztery mają okno 1M tokenów. Ceny i domyślność potwierdza changelog Claude Code.

Szczegóły:
- **Opus 5.5**: według Anthropic zadania kosztują ogólnie około 40% mniej niż na Opus 5. Model generuje odpowiedź ponad 30% szybciej.
- **Sonnet 5.5**: Anthropic opisuje go jako wyraźny skok względem Sonnet 5. Jest ponad 30% szybszy i do 30% tańszy w większości zadań. W GDPval-AA traci 2 punkty do Opus 5.5.
- **Haiku 5.5**: według Anthropic działa średnio około 75% taniej niż Haiku 4.5. To pierwszy Haiku z regulowanym wysiłkiem (effort). Powyżej 100K tokenów promptu kosztuje $0.50 / $2.50. Tego samego dnia Anthropic obniżył o połowę cenę odczytu cache dla Sonnet 5.5, do $0.10/Mtok.

## Oś czasu

- **2026-05-06**: limity Claude Code wyższe na stałe (patrz niżej). Anthropic ogłosił też umowę na moc obliczeniową ze SpaceX: ponad 300 MW, ponad 220 000 GPU NVIDIA.
- **2026-05-28**: Claude Opus 4.8.
- **2026-06-09**: **Claude Fable 5**, pierwsza publiczna wersja modelu Mythos. Mythos ogłoszono 7 kwietnia 2026, ale udostępniono go tylko partnerom. W ryzykownych dziedzinach (cyberbezpieczeństwo, biologia, chemia) Fable odmawia i przełącza się na Opus 4.8. Cena $10 / $50. Model zniknął po kilku dniach przez dyrektywę eksportową rządu USA i wrócił 2026-07-01 z dodatkowymi klasyfikatorami.
- **2026-06-30**: **Claude Sonnet 5**, za $2 / $10. Zastąpił Sonnet 4.6 jako domyślny model na Free i Pro. Cena miała być promocyjna, ale Anthropic w sierpniu ogłosił, że zostaje na stałe.
- **2026-07-24**: **Claude Opus 5** za $5 / $25. Domyślny model dla Max. Ma wybór wysiłku (low / medium / high). Według Anthropic „comes close” do Fable 5 za połowę ceny.
- **2026-09-01**: Claude Fable 5.1 i Mythos 5.1.
- **2026-09-16**: Claude Docs, Slides i Design w becie, w zwykłej rozmowie, na płatnych planach.
- **2026-09-22**: **Claude Opus 5.5**, pierwszy model rodziny 5.5. Do tego wyższe limity 5-godzinne.
- **2026-09-28**: **Claude Sonnet 5.5**.
- **2026-10-07**: **Claude Haiku 5.5**. Anthropic pominął „Haiku 5”.
- **2026-10-08**: Docs, Slides i Design wyszły z bety na wszystkich planach, także Free. Nowe produkty to **Claude Dashboards** (beta, płatne plany), czyli dashboardy z podłączonych danych (Snowflake, Databricks, BigQuery, Salesforce), oraz **Claude Motion** (beta, Team i Enterprise): krótkie animacje z promptu, edytowalne jako kod, eksport do MP4, komenda `/motion`. Ogłoszono też zamknięcie osobnej strony Claude Design.

## Produkty

- **Claude Design**: projekty i design systemy w zwykłej rozmowie, w Claude Code i w zakładce Artifacts. Osobna strona claude.ai/design zamyka się **2026-12-14**. Potem jest tylko do odczytu, a jej adres prowadzi do Claude. Design systemy trzeba przenieść samemu przed tą datą. Puste systemy i systemy zrobione z gotowego motywu startowego się nie przeniosą. Rozmowy i komentarze zostaną usunięte, a publiczne linki do projektów przestaną działać.
- **Claude Docs i Slides**: dokumenty i prezentacje w rozmowie. Od 2026-10-08 na wszystkich planach.
- **Claude Dashboards i Motion**: opisane wyżej, w osi czasu pod 2026-10-08.
- **Claude Code**: patrz [Claude Code — stan obecny i ostatnie zmiany](claude-code.md).

## Limity na planach Pro i Max

- **2026-03-26**: w godzinach szczytu w dni robocze limity 5-godzinne zużywały się szybciej. Źródło: blog zewnętrzny, wiarygodność low.
- **2026-05-06**: Anthropic na stałe podwoił 5-godzinne limity Claude Code na Pro, Max, Team i Enterprise z licencją na stanowisko. Zniósł też obniżkę w godzinach szczytu dla Pro i Max.
- **Maj–wrzesień 2026**: tymczasowo tygodniowe limity Claude Code były o 50% wyższe. Według pomocy Anthropic od 2026-09-14 są na stałe o 25% wyższe niż przed promocją. Źródło: blog zewnętrzny, który cytuje centrum pomocy, wiarygodność low.
- **2026-09-22**: razem z Opus 5.5 przyszły wyższe limity 5-godzinne i jeden reset limitu, który zapisujesz i używasz, kiedy chcesz. Anthropic nie podał nowych liczb.

> **Status: Disputed**: proporcje między planami. Według oficjalnego opisu Max 20x daje 20 razy więcej niż Pro. Jeden zewnętrzny pomiar szacuje około 10 razy (explainx.ai, wiarygodność low).

## Jak stosować

- Do większości kodowania wystarczy Sonnet 5.5. Opus 5.5 włączaj do trudnych decyzji i architektury. Haiku 5.5 dawaj subagentom i masowym, prostym zadaniom.
- W API po 22 września przejdź na modele 5.5. Są tańsze od 5, a Haiku 5.5 kosztuje ułamek Haiku 4.5.
- Masz zapisany reset limitu z 22 września? Użyj go, gdy limit skończy się w ważnym momencie.
- Przenieś design systemy z claude.ai/design przed 2026-12-14.

## Zobacz też
- [Claude Code — stan obecny i ostatnie zmiany](claude-code.md) — zmiany w Claude Code wersja po wersji
- [Wytyczne Anthropic do designu frontendu z Claude](../design/anthropic-frontend-design.md) — Claude Design od strony designu
