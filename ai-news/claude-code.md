---
title: Claude Code — stan obecny i ostatnie zmiany
updated: 2026-10-28
tags: [claude-code, anthropic, agents, cli, changelog]
sources:
  - "[anthropics/claude-code CHANGELOG.md](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) — 2026-10-27 — high"
  - "[anthropics/claude-code releases](https://github.com/anthropics/claude-code/releases) — 2026-10-27 — high"
  - "[Move from standalone Claude Design to Claude (support.claude.com)](https://support.claude.com/en/articles/17440474-move-from-standalone-claude-design-to-claude) — 2026-10-08 — high"
  - "[Higher usage limits and a SpaceX compute deal (Anthropic)](https://www.anthropic.com/news/higher-limits-spacex) — 2026-05-06 — high"
---

# Claude Code — stan obecny i ostatnie zmiany

> Claude Code to agent kodujący Anthropic: działa w terminalu, w aplikacji desktop, w przeglądarce i w IDE. Od maja do października 2026 wydał około 190 wersji (od 2.1.126 do 2.1.312). Najważniejsze zmiany: widok wszystkich sesji (`claude agents`), sesje w tle, dynamiczne workflowy (`ultracode`), `/goal`, auto mode, Mods (plugin może zmieniać głębsze zachowanie), czytanie `AGENTS.md`, nowe domyślne modele z rodziny 5.5 i Claude Design w Claude Code.

## Co to jest teraz

Najważniejsze możliwości według changelogu (stan na 2.1.312, 2026-10-27):

- **Wiele sesji naraz.** `claude agents` pokazuje listę wszystkich sesji: działających, czekających na Ciebie i skończonych. Sesje mogą działać w tle (`claude --bg`). Masz do tego `claude attach <name>`, `claude logs <name>`, `stop`, `respawn` i `rm`.
- **Sesje rozmawiają ze sobą.** `SendMessage` działa między sesjami, także na Twoich innych maszynach. `ListAgents` znajduje inne sesje.
- **Dynamiczne workflowy.** Claude rozdziela dużą pracę na wielu agentów naraz. Słowo-wyzwalacz to `ultracode`, wcześniej było nim `workflow`. Rozmiar workflowu ustawiasz w `/config` („Dynamic workflow size”).
- **Praca do celu.** `/goal` ustala warunek końca, a Claude pracuje przez kolejne tury, aż go spełni. `/loop` uruchamia zadanie cyklicznie.
- **Auto mode.** Klasyfikator sam zatwierdza bezpieczne akcje zamiast pytać Cię o każdą. Ma regułę `hard_deny`, zakładkę w `/permissions` i komendę `/auto-mode-setup` z prowadzoną konfiguracją.
- **Rozszerzenia.** Rozszerzają go pluginy, skille, hooki, MCP i od października Mods: plugin może zmieniać głębsze zachowanie i rysować własny interfejs. Do tego dochodzą `claude plugin eval` (testy pluginów) i `/skill-doctor` (które skille nie są używane i ile kosztują kontekstu).
- **Instrukcje projektu.** Jeśli projekt nie ma `CLAUDE.md`, Claude Code czyta `AGENTS.md`.
- **Modele.** Domyślne są teraz Opus 5.5, Sonnet 5.5, Haiku 5.5 i Fable 5.1 (patrz [Anthropic — modele, produkty i limity (maj–październik 2026)](anthropic.md)). `/advisor` dodaje drugi model jako doradcę. Jest też fast mode i poziom wysiłku `/effort`.
- **Kontekst i koszty.** Idle compaction zwija długą rozmowę przed wygaśnięciem cache. `/cost` pokazuje trafienia cache i przyczyny chybień. `/usage` ostrzega przed drogimi ustawieniami.
- **Interfejs.** Ma tryb pełnoekranowy z obsługą myszy, panel diffu (`/diff`) i widok `/focus`. Ma też wbudowany styl odpowiedzi „Concise”.

## Ostatnie zmiany

Od najnowszych. Tylko rzeczy, które zmieniają codzienną pracę.

**Październik 2026**
- 2026-10-19 (2.1.304): `/auto-mode-setup` czyta projekt i ostatnie sesje, żeby nauczyć auto mode Twojego środowiska. Na planach Pro i Max pojawia się ostrzeżenie, gdy wznowienie starej rozmowy zje dużą część limitu 5-godzinnego.
- 2026-10-16 (2.1.302): `/design-sync` i `/design-login` ostrzegają, że osobna strona Claude Design (claude.ai/design) zamyka się 14 grudnia 2026. Design działa już w zwykłej rozmowie i w Claude Code.
- 2026-10-14 (2.1.299): idle compaction. Rozmowa powyżej 200K tokenów, bezczynna około 54 minut, zostaje zwinięta, zanim wygaśnie godzinny cache. Wyłączysz to przez `"idleCompaction": false`. `/usage` ostrzega przed max effort, workflowami i dużymi wynikami narzędzi.
- 2026-10-07 (2.1.293): Claude Haiku 5.5 został domyślnym Haiku.
- 2026-10-02 (2.1.288): Ctrl+C czyści prompt, a strzałka w górę go przywraca. `/code-review --max-findings <n>|all` zmienia liczbę zgłoszeń w review.
- 2026-10-01 (2.1.287): **Claude Mods**, czyli pluginy, które zmieniają głębsze zachowanie Claude Code. Do tego wbudowany mod „You should know”: boczny agent pilnuje rzeczy, które Ty albo Claude możecie przeoczyć.

**Wrzesień 2026**
- 2026-09-28 (2.1.284): Claude Sonnet 5.5 został domyślnym Sonnetem. `/mcp reconnect all` łączy ponownie wszystkie serwery MCP.
- 2026-09-25 (2.1.283): `/doctor prompt-audit` sprawdza Twoje `CLAUDE.md`, skille, agentów i komendy. Szuka wzorców pisanych pod starsze modele.
- 2026-09-22 (2.1.280): Claude Opus 5.5 został domyślnym Opusem.
- 2026-09-18 (2.1.277): **wsparcie `AGENTS.md`**. W projekcie bez `CLAUDE.md` Claude Code czyta `AGENTS.md`. Zmienisz to w `/config` („Project instructions”).
- 2026-09-17 (2.1.275): skille i pluginy włączone na koncie claude.ai synchronizują się z terminalem. Wyłączysz to przez `syncClaudeAiSkills: false`. Nowy klawisz wysyłki (ctrl+enter) przerywa turę i wysyła wszystkie wiadomości z kolejki.
- 2026-09-11 (2.1.269): `claude plugin eval` uruchamia testy pluginu i daje raport JSON i HTML. Nowy widok `/focus` pokazuje tylko prompt, podsumowanie pracy i odpowiedź.
- 2026-09-04 (2.1.261): `/skill-doctor` pokazuje nieużywane skille i ich koszt w kontekście.
- 2026-09-03 (2.1.260): panel diffu obok rozmowy (`/diff`). `/cost` podaje prawdopodobną przyczynę chybienia cache.
- 2026-09-01 (2.1.257): Claude Fable 5.1 został domyślnym Fable. Nowe ustawienia `timeFormat` i `timeZone`.

**Sierpień 2026**
- 2026-08-28 (2.1.251): hooki `PreModelSwitch` i `PostModelSwitch`. `/cost` pokazuje statystyki prompt cache.
- 2026-08-25 (2.1.246): zakładka „Auto mode” w `/permissions` z regułami klasyfikatora.
- 2026-08-20 (2.1.237): wbudowany styl odpowiedzi „Concise”. Claude zaczyna od wyniku i nie opowiada, co robi.
- 2026-08-17 (2.1.234): sesja sama rusza dalej po resecie limitu claude.ai. Wyłączysz to w `/config`.
- 2026-08-07 (2.1.224): `SendMessage` między sesjami, także na innych maszynach. Pluginy można instalować z archiwum zip przez HTTPS.

**Lipiec 2026**
- 2026-07-24 (2.1.219): Claude Opus 5 został domyślnym Opusem. Nowe ustawienie `sandbox.network.strictAllowlist`.
- 2026-07-10 (2.1.206): `/doctor` proponuje skrócenie `CLAUDE.md` o treść, którą Claude wyczyta z kodu.
- 2026-07-06 (2.1.202): ustawienie „Dynamic workflow size” (small/medium/large).
- 2026-07-01 (2.1.198): powiadomienia z sesji w tle w `claude agents` oraz skill `/dataviz` z zasadami wykresów.

**Czerwiec 2026**
- 2026-06-24 (2.1.191): `/rewind` potrafi wrócić do rozmowy sprzed `/clear`.
- 2026-06-17 (2.1.181): `/config key=value` ustawia dowolne ustawienie z promptu, np. `/config thinking=false`.
- 2026-06-15 (2.1.178): reguły uprawnień po parametrach narzędzia, np. `Agent(model:opus)`.
- 2026-06-08 (2.1.169): `/cd` przenosi sesję do innego katalogu bez utraty cache.
- 2026-06-06 (2.1.166): `fallbackModel` ustawia do trzech zapasowych modeli na wypadek przeciążenia.
- 2026-06-02 (2.1.160): słowo-wyzwalacz dynamicznego workflowu zmienione z `workflow` na `ultracode`.

**Maj 2026**
- 2026-05-27 (2.1.152): `/reload-skills` wczytuje skille bez restartu. Nowy hook `MessageDisplay`.
- 2026-05-19 (2.1.144): `/resume` obejmuje sesje działające w tle.
- 2026-05-11 (2.1.139): **agent view** (`claude agents`, Research Preview) i **`/goal`**. `claude plugin details` pokazuje koszt pluginu w tokenach.
- 2026-05-06: Anthropic na stałe podwoił 5-godzinne limity Claude Code na planach Pro, Max, Team i Enterprise. Zniósł też obniżkę limitów w godzinach szczytu dla Pro i Max (szczegóły w [Anthropic — modele, produkty i limity (maj–październik 2026)](anthropic.md)).

## Jak stosować

Rzeczy warte włączenia albo wypróbowania:
- `claude agents`: widok wszystkich sesji. Przydaje się, gdy prowadzisz kilka zadań naraz.
- `/goal <warunek>` przy dłuższym zadaniu, np. „wszystkie testy przechodzą”.
- `/auto-mode-setup`, a potem auto mode. Dostajesz mniej pytań o uprawnienia.
- `/skill-doctor` i `/doctor prompt-audit`: porządki w skillach i `CLAUDE.md`. Usuwasz to, co nieużywane albo pisane pod stare modele.
- `/cost`: sprawdzisz, czy cache działa. Przy długich sesjach zostaw idle compaction włączone.
- `/config key=value`: szybka zmiana ustawień bez otwierania panelu.
- Gdy repo ma tylko `AGENTS.md`, Claude Code czyta go sam (tak działa Cortex).
- Masz projekty w claude.ai/design? Przenieś design systemy przed 14 grudnia 2026.

Nowości śledzisz przez `https://github.com/anthropics/claude-code/releases.atom` (RSS) albo `CHANGELOG.md` w tym repo.

## Zobacz też
- [Anthropic — modele, produkty i limity (maj–październik 2026)](anthropic.md) — modele, ceny, limity i inne produkty Anthropic
- [Wytyczne Anthropic do designu frontendu z Claude](../design/anthropic-frontend-design.md) — Claude Design i skille do designu
