---
title: Jak uniknąć designu, który wygląda na wygenerowany przez AI
updated: 2026-10-28
tags: [ai-slop, frontend, typografia, kolor, ruch, checklista]
sources:
  - "[anthropics/skills — frontend-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) — 2026-09-03 — high"
  - "Claude built-in skill artifact-design — unknown — high"
  - "[Prompting for frontend aesthetics (Claude Cookbook)](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics) — 2025-10-21 — high"
  - "[Improving frontend design through Skills (claude.com)](https://claude.com/resources/articles/improving-frontend-design-through-skills) — 2025-11-12 — high"
  - "[pbakaus/impeccable — reference/craft-floor.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/craft-floor.md) — unknown — high"
  - "[pbakaus/impeccable — reference/new-work.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/new-work.md) — unknown — high"
  - "[leonxlnx/taste-skill — SKILL.md (house rules)](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/SKILL.md) — unknown — medium"
---

# Jak uniknąć designu, który wygląda na wygenerowany przez AI

> Design z AI skupia się wokół kilku powtarzalnych wyglądów i drobnych „tików” (eyebrow w ALL CAPS, `·` między metadanymi, `→` w przyciskach, karty z tym samym cieniem). Każdy z nich bywa dobry dla konkretnego briefu, ale pojawia się niezależnie od tematu, więc zdradza brak decyzji. Zasada Anthropic: gdy brief określa kierunek, wykonaj go dokładnie; gdy zostawia oś wolną, nie wydawaj tej wolności na domyślny wybór.

## Pięć klastrów designu z AI (frontend-design, 2026-09)

1. Ciepłe kremowe tło (około `#F4F1EA`), kontrastowy szeryf display i akcent terakota/glina (często około `#D97757` — to akcent samego Claude, więc w cudzym projekcie zdradza AI).
2. Prawie czarne tło z jednym jaskrawym akcentem: kwasowa zieleń albo cynober.
3. Układ „broadsheet”: włosowe linie, zero zaokrągleń, gęste kolumny jak w gazecie.
4. „SaaS-card kit”: treść pocięta na identyczne zaokrąglone karty, jeden radius na wszystkim, ten sam miękki szary cień (`rgba(0,0,0,.1)`), gradientowe plamy jako dekoracja.
5. „Template chrome” niezależny od tematu:
   - rozstrzelona etykieta ALL CAPS nad każdym nagłówkiem,
   - metadane łączone kropką środkową (`A · B · C`),
   - etykiety w formie `WORD — fragment` z pauzą,
   - lekko zabarwiona prawie-czerń (`#0B0B0B`, `#111`) zamiast czerni,
   - monospace dla małych etykiet danych,
   - `→` doklejona do linków i przycisków.

Artifact-design dokłada: fioletowo-niebieski gradient hero na białym, Inter lub Space Grotesk jako „bezpieczny” krój, emoji jako znaczniki sekcji, wszystko wyśrodkowane, `rounded-lg` wszędzie, pasek akcentu na zaokrąglonych kartach.

`impeccable` opisuje trzy z tych klastrów tak samo i dodaje czwarty: **płaski nasycony tusz, czarne ramki, twarde przesunięte cienie i ciężki wąski krój display**. To neobrutalizm jako kostium. Wszystkie klastry są dobre, gdy brief ich chce.

## Lista odmowy (impeccable craft-floor, taste-skill)

Domyślne wybory kategorii. Brief może każdy z nich uzasadnić. Sięganie po nie, gdy oś jest wolna, znaczy, że nie podjąłeś decyzji:
- identyczne karty „ikona + nagłówek + tekst” jako struktura strony. Karty zagnieżdżone w kartach są zawsze złe;
- szablon „hero z metryką”: duża liczba, mała etykieta, statystyki pomocnicze, akcent;
- gradient w tekście;
- szkło i blur jako dekoracja;
- kolorowy `border-left` szerszy niż 1px na kartach i alertach;
- twarde cienie `box-shadow: 4px 4px 0` poza światem neobrutalistycznym;
- sparkline'y, pierścienie postępu i zaokrąglone prostokąty z miękkim cieniem zamiast treści;
- monospace jako kostium „techniczności”, a nie do kodu i danych;
- znaki Unicode albo emoji zamiast systemu ikon. Ikony mają być z biblioteki albo z własnego SVG, o jednej grubości kreski;
- geometryczne maski (koło, wielokąt) udające kontur zdjęcia;
- systemowy krój display (Impact, Arial Black) na stronie z własnym światem;
- modal tam, gdzie zadanie nie wymaga przerwania.

Eyebrow nad nagłówkiem `impeccable` uznaje za zakaz bez wyjątków. Żaden brief go nie uzasadnia.

`taste-skill` idzie dalej i zakazuje na każdej stronie: eyebrow, monospace poza kodem, numeracji 01/02/03, cienkich linii i obramowań 1px, gradientów, cieni na elementach w spoczynku, fioletu i indygo, kremu z terakotą, wyróżnionego słowa w nagłówku, szkła i pływającej nawigacji w pigułce oraz więcej niż dwóch krojów. Autorzy podają liczby z badania 247 stron. Strony z oceną 7.5+ użyły kart funkcji z ikoną w 1% przypadków, a strony poniżej 6.5 w 28%. Badge w pigułce: 14% kontra 34%. Gradienty: 22% kontra 52%. Cienie: 24% kontra 48%. Drobne rozstrzelone wersaliki: 16% kontra 57%. Monospace, numeracja i włosowe siatki są według autorów częstsze na nagrodzonych stronach. Zakazali ich, bo generatory je naśladują i dziś wyglądają jak kostium. To opinia autorów, nie wynik badania.

> **Uwaga z testów taste-skill:** usunięcie ozdobników to połowa pracy. Strona, która straciła etykiety, linie i karty, ale nic w zamian nie zyskała, jest pusta. W ślepych testach jurorzy woleli bogatszą stronę z tikami. Wolne miejsce wypełnij skalą, pełną treścią, obrazem zrobionym dla tematu albo polem koloru. Nie wypełniaj go innym ozdobnikiem.

## Typografia

- Nie wyróżniaj jednego słowa w nagłówku (kursywa, pogrubienie, inny kolor).
- Nie rób etykiet w ALL CAPS.
- Nie dodawaj zbędnych etykiet nad treścią.
- Typografia nagłówka ma być aktywną częścią designu, nie neutralnym nośnikiem.
- Krój wybieraj świadomie dla tematu, nie z odruchu.

> **Status: Outdated** (2026-10-28) — Cookbook z 2025-10-21 podawał gotowe listy krojów zastępczych (np. „Code aesthetic: JetBrains Mono, Fira Code, Space Grotesk”, „Editorial: Playfair Display, Crimson Pro, Fraunces”) i zakaz „Inter, Roboto, Open Sans, Lato, default system fonts”. Już ten sam prompt zauważał, że Claude „still tend[s] to converge on common choices (Space Grotesk, for example)”. Wersja skilla z 2026-09-03 nie podaje list; każe wybierać krój z tematu. Artifact-design wprost wymienia Inter i Space Grotesk jako znaki AI. Listy z 2025 traktuj jako inspirację, nie jako bezpieczny wybór.

## Kolor i tło

- Neutrale wybieraj celowo. Czysta średnia szarość wygląda na niedopracowaną. Szarość lekko podbarwiona w stronę akcentu wygląda na zamierzoną (artifact-design).
- „Dominant colors with sharp accents outperform timid, evenly-distributed palettes” (cookbook 2025).
- Jeśli akcent gryzie się z tłem, przesuń go w stronę barwy analogicznej albo zdesaturuj. Nie wymieniaj go.
- Cookbook 2025 zalecał tła z atmosferą (warstwy gradientów, wzory geometryczne). Skill 2026 każe ciąć dekorację, która nie służy briefowi, i wymienia „gradient washes as decoration” jako tik. Tło z atmosferą — tak, jeśli wynika z tematu.

## Layout i struktura

- Karty, obramowania, cienie i radius stosuj według roli, do wyróżnienia jednego elementu. Ten sam radius i cień na wszystkim spłaszcza hierarchię.
- Numerowanie 01 / 02 / 03 tylko dla prawdziwej sekwencji (proces, oś czasu).
- Hero z dużymi liczbami tylko wtedy, gdy liczby są sednem strony.
- Hero dopasowany do treści, nie `100vh` — inaczej reszta strony wypada z pierwszego kadru.

## Ruch

> **Status: Disputed** — Cookbook 2025: „one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions”. Skill 2026: „fade-and-slide-up entrances on each section and hover transitions on every card are the generic default and read as AI-generated”. Oba zgadzają się co do jednego zaaranżowanego momentu; różnią się tym, że w 2026 wjazd każdej sekcji jest już uznany za tik.

- Treść ma być widoczna po załadowaniu, bez scrollowania. Sekcja może się animować, ale z widocznego stanu, nigdy z `opacity: 0` czekającej na IntersectionObserver.
- Zawsze respektuj `prefers-reduced-motion`.
- Spór między skillami o ilość ruchu na stronach marketingowych i zasady animacji UI → [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md).

## Tekst (copy)

- Pisz z perspektywy użytkownika: „powiadomienia”, nie „konfiguracja webhooków”.
- Strona czynna. Przycisk mówi, co się stanie: „Zapisz zmiany”, nie „Wyślij”. Ta sama nazwa w całym przepływie: „Opublikuj” → toast „Opublikowano”.
- Błędy mówią, co poszło źle i jak to naprawić. Bez przeprosin i ogólników.
- Bez manier: wtrąceń w pauzach, „nie X, tylko Y”, dwukropka z puentą, cudzysłowów wokół wymyślonych etykiet.

## Jak stosować

Checklista przed oddaniem projektu (wklej modelowi albo przejdź sam):

```
Sprawdź projekt i dla każdego punktu odpowiedz TAK/NIE + gdzie:
1. Czy paleta to któryś z klastrów: krem+szeryf+terakota, czerń+kwasowy akcent,
   broadsheet z włosowymi liniami, fiolet-niebieski gradient na białym?
2. Czy wszystkie bloki to identyczne karty z tym samym radius i cieniem?
3. Czy jest eyebrow ALL CAPS nad nagłówkami, "A · B · C", "→" w przyciskach,
   monospace w małych etykietach, emoji jako znaczniki sekcji?
4. Czy w nagłówku jedno słowo jest wyróżnione kolorem/kursywą?
5. Czy font to Inter / Space Grotesk / Roboto bez powodu w briefie?
6. Czy numeracja 01/02/03 opisuje prawdziwą sekwencję?
7. Czy każda sekcja wjeżdża fade-and-slide-up, a każda karta ma hover?
8. Czy treść jest widoczna bez scrollowania (brak opacity:0 do observera)?
9. Czy jest jeden zapamiętywalny element, a reszta spokojna?
Każde TAK, które nie wynika z briefu, zamień na wybór wynikający z tematu.
```

## Zobacz też
- [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) — skąd te zasady i jaki proces za nimi stoi
- [Prompty do sterowania estetyką designu](design-prompting.md) — jak od początku sterować estetyką promptem
- [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) — pełne rubryki przeglądu i limity punktów za tiki
- [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md) — jak wybrać kierunek z tematu zamiast z kategorii
