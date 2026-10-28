---
title: Wytyczne Anthropic do designu frontendu z Claude
updated: 2026-10-28
tags: [anthropic, claude, frontend, design, skills, proces]
sources:
  - "[anthropics/skills — frontend-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) — 2026-09-03 — high"
  - "[Prompting for frontend aesthetics (Claude Cookbook, Prithvi Rajasekaran)](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics) — 2025-10-21 — high"
  - "[Improving frontend design through Skills (claude.com)](https://claude.com/resources/articles/improving-frontend-design-through-skills) — 2025-11-12 — high"
  - "Claude built-in skill artifact-design — unknown — high"
  - "[anthropics/skills — canvas-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/canvas-design/SKILL.md) — unknown — high"
  - "[Anthropic launches Claude Design (TechCrunch)](https://techcrunch.com/2026/04/17/anthropic-launches-claude-design-a-new-product-for-creating-quick-visuals/) — 2026-04-17 — medium"
  - "[Claude Design in 2026: Features, Access and Limits (agence-scroll)](https://agence-scroll.com/en/blog/claude-design-anthropic-2026-guide) — unknown — low"
---

# Wytyczne Anthropic do designu frontendu z Claude

> Anthropic mówi wprost: model bez wskazówek wybiera „bezpieczny środek” danych treningowych, więc projekty wyglądają generycznie („AI slop”). Lekarstwo to krótkie, celowane wytyczne ładowane tylko przy zadaniach frontendowych (Skill `frontend-design`). Obecna wersja skilla (wrzesień 2026) stawia na proces: zakotwicz projekt w temacie, zrób plan tokenów, porównaj go z generycznym domyślnym, dopiero potem koduj i oceniaj zrzuty ekranu.

## Problem: distributional convergence

- Model przewiduje tokeny według wzorców z danych. „Safe design choices–those that work universally and offend no one–dominate web training data.” Bez kierunku Claude losuje z tego środka: Inter, fioletowe gradienty na białym, minimalna animacja.
- Claude jest sterowalny. Konkretne polecenie („avoid Inter and Roboto”, „use atmospheric backgrounds instead of solid colors”) od razu poprawia wynik.
- Wniosek z artykułu: model umie więcej, niż pokazuje domyślnie.

## Dlaczego Skill, a nie system prompt

- Pełne wytyczne (typografia, kolor, ruch, tła) w system prompcie obciążałyby każde zadanie, także debugowanie Pythona. Artykuł zauważa, że „too many tokens in the context window can result in degradation of performance”.
- Skill ładuje się tylko przy zadaniu frontendowym. Prompt estetyczny ma około 400 tokenów.
- Osobny skill `web-artifacts-builder` pozwala budować wieloplikowe artefakty w React, Tailwind i shadcn/ui, a potem pakuje je Parcelem do jednego pliku HTML.

## Ewolucja wytycznych

| Data | Źródło | Akcent |
|---|---|---|
| 2025-10-21 | Cookbook „Prompting for frontend aesthetics” | lista „nie używaj” fontów, listy fontów zastępczych, odważne kolory, staggered reveal |
| 2025-11-12 | Artykuł „Improving frontend design through Skills” + plugin `frontend-design` | ten sam ~400-tokenowy prompt jako Skill |
| 2026-06-09, 2026-09-03 | Aktualizacje `frontend-design` SKILL.md | proces dwuprzebiegowy, katalog 5 typowych „klastrów” AI, mniej list fontów, więcej osądu |
| 2026-04-17 | Claude Design (Anthropic Labs) | osobny produkt do prototypów, slajdów i one-pagerów |

## Zasady z obecnego `frontend-design` (2026-09)

**Postawa.** Działaj jak „design lead at a design studio known for giving every client a distinct visual identity”. Klient odrzucił już szablonowe propozycje.

**Temat.** Jeśli brief nie mówi, czego dotyczy produkt, określ sam: jeden konkretny temat, odbiorcę i główne zadanie strony. Branża, materiały i słownictwo tematu to źródło wyrazistych wyborów.

**Hero.** Otwórz najbardziej charakterystyczną rzeczą ze świata tematu. Duża liczba z małą etykietą, statystyki i gradientowy akcent to domyślny wzór. Używaj go tylko, gdy naprawdę jest najlepszy.

**Typografia.**
- Jedna albo dwie rodziny. Jeśli dwie, to wyraźnie różne.
- Świadomy wybór kroju, nie „domyślne” rodziny. Skala typograficzna według „The Elements of Typographic Style”.
- Linie tekstu poniżej 80 znaków. Szeryfy mogą mieć trochę dłuższe linie i większą interlinię.
- Artifact-design doprecyzowuje: tekst ciągły około 65 znaków, nagłówki `text-wrap: balance`.

**Struktura to informacja.** Obramowania, numeracja, eyebrow, separatory muszą coś znaczyć. Numerki 01 / 02 / 03 tylko dla prawdziwej sekwencji.

**Ruch.** Oszczędnie. Jeden zaaranżowany moment działa lepiej niż rozproszone efekty. Ruch w odpowiedzi na akcję użytkownika (otwarcie, rozwinięcie, potwierdzenie) jest mile widziany.

**Powściągliwość.** „Spend your boldness in one place.” Jeden element ma być zapamiętywalny, reszta spokojna. Rada Chanel: przed wyjściem zdejmij jeden dodatek.

**Podłoga jakości (bez ogłaszania jej).** Responsywność do mobile, widoczny fokus klawiatury, `prefers-reduced-motion`, dostępny kontrast.

**CSS.** Pilnuj specyficzności selektorów. Klasy typu `.section` i `.cta` łatwo kasują sobie nawzajem padding i marginesy.

## Proces: plan → przegląd → budowa → krytyka

1. **Plan (kompaktowy system tokenów):**
   - Kolor: 4–6 nazwanych wartości hex.
   - Typ: kroje i ich role.
   - Layout: koncepcja w jednym zdaniu plus ASCII wireframe; wyrównanie (lewo, środek, justowanie).
   - Zasady: co czyni tę stronę wyjątkową.
2. **Przegląd planu względem briefu.** Jeśli coś wygląda jak domyślny wybór dla każdej podobnej strony, zmień to i powiedz, co i dlaczego. Test: przejdź w głowie podobny prompt i sprawdź, czy dochodzisz w to samo miejsce.
3. **Budowa** dokładnie według poprawionego planu.
4. **Krytyka na zrzutach ekranu.** „A picture is worth 1000 tokens.” Notuj, co już próbowałeś, żeby kolejne projekty nie powtarzały się.

## Pozostałe skille i narzędzia Anthropic

- **canvas-design** (plakaty, grafika statyczna PNG/PDF): najpierw „filozofia wizualna” jako manifest ruchu artystycznego (nazwa w 1–2 słowach, 4–6 akapitów), potem ekspresja na płótnie: 90% wizualnie, 10% tekstu. Mocny nacisk na „master-level execution”.
- **brand-guidelines**: skill z identyfikacją marki Anthropic (przykład, jak zapisać własny design system jako skill).
- **artifact-design** (wbudowany w Claude): te same zasady co `frontend-design` plus reguły techniczne: oba motywy (jasny i ciemny) na poziomie tokenów, layout przez `gap`, strona kompletna bez scrollowania i bez `opacity: 0` czekającej na observer, Google Fonts z prawdziwym fallbackiem.
- **Claude Design** (Anthropic Labs, premiera 2026-04-17): prototypy, slajdy, one-pagery z rozmowy. Poprawki przez rozmowę, komentarze, edycję i suwaki generowane przez Claude. Czyta design system z kodu i plików. Eksport do Canva, PDF, PPTX, HTML. Przekazanie do Claude Code. Według przewodnika agence-scroll od września 2026 jest betą dostępną też w czacie i Claude Code (źródło niskiej wiarygodności).

## Jak stosować

1. W Claude Code zainstaluj skill: `anthropics/skills` → `frontend-design` (albo plugin `frontend-design` z oficjalnego marketplace).
2. W briefie podaj temat, odbiorcę i główne zadanie strony. Bez tego model zgaduje środek rozkładu.
3. Poproś najpierw o plan tokenów, nie o kod:

```
Zanim napiszesz kod, daj plan: 4–6 kolorów hex z nazwami, kroje i ich role,
koncepcję layoutu w jednym zdaniu + ASCII wireframe, 2–3 zasady wyróżniające.
Potem sprawdź plan: co w nim wygląda jak domyślny wybór dla dowolnej podobnej
strony? Zmień to i napisz, co zmieniłeś. Dopiero potem koduj.
```

4. Po zbudowaniu każ zrobić zrzut ekranu (desktop + mobile) i jedną rundę poprawek.
5. Sprawdź wynik listą z [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md).

## Zobacz też
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — konkretne „znaki rozpoznawcze” designu z AI
- [Prompty do sterowania estetyką designu](design-prompting.md) — gotowe prompty i techniki sterowania estetyką
- [Katalog popularnych skilli do designu (skills.sh)](design-skills-catalog.md) — inne popularne skille do designu ze skills.sh
