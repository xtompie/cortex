---
title: Proces projektowania strony z LLM — od pytań do krytyki
updated: 2026-10-28
tags: [process, frontend, design, prompting, checklist]
sources:
  - "[Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md)"
  - "[Prompty do sterowania estetyką designu](design-prompting.md)"
  - "[Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md)"
  - "[Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md)"
  - "[Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md)"
  - "[Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md)"
  - "[Podstawy web designu dla developera](web-design-fundamentals.md)"
  - "[Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md)"
  - "[Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md)"
  - "[DESIGN.md — design system w jednym pliku dla agenta](design-md.md)"
---

# Proces projektowania strony z LLM — od pytań do krytyki

> Siedem kroków: pytania → idea i kierunki → plan tokenów → przegląd planu → budowa (najpierw słowa, ruch na końcu) → przegląd na zrzutach → zapis kierunku. Bez briefu model wybiera bezpieczny środek kategorii. Dlatego najpierw zbiera brief od człowieka i buduje ideę z rzeczy, które ma tylko ten temat. Dopiero potem planuje i koduje. Ta strona składa w jeden proces zasady z pozostałych stron `design`.

## Kroki

**1. Pytania (brief).** Zanim cokolwiek zaprojektujesz, zapytaj człowieka. Jedna wiadomość, krótkie pytania, maksymalnie 6:
- Czego dotyczy strona? Jeden konkretny temat albo produkt.
- Kto jest odbiorcą i w jakiej sytuacji używa strony?
- Jakie jest jedno główne zadanie strony? Co odbiorca ma zrobić albo zrozumieć? Po czym poznamy sukces?
- Jakie materiały naprawdę istnieją: zdjęcia, zrzuty produktu, logo, treści? Nie planuj obrazów, których nie ma (`taste-skill`).
- Czego nie ruszać i co sprawiłoby, że dopracowany wynik będzie „nie taki”? (`impeccable`)
- Ograniczenia: istniejący design system, kolory marki, stack (Tailwind, shadcn), czy ma być dark mode. Opcjonalnie nastrój albo wzory.

Z typu ekranu wywnioskuj tryb: Persuade, Operate, Read albo Experience ([Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md)). Dopytaj tylko, gdy nie jest oczywisty. Nie pytaj o wartości CSS ani o gotowe szufladki stylu (`impeccable`).

Jeśli projekt ma już `DESIGN.md`, tokeny albo style komponentów, przeczytaj je przed pytaniami i nie pytaj o to, co w nich jest. Kolejność ważności: słowa człowieka, potem istniejący design system, dopiero potem wybory modelu ([Prompty do sterowania estetyką designu](design-prompting.md)). Nowa sekcja w istniejącym świecie dziedziczy ten świat. Nie zaczynaj dla niej nowego kierunku.

> Pytania to decyzja Cortex. Źródła się tu różnią. Anthropic `frontend-design` przy braku briefu każe modelowi samemu wybrać temat i odbiorcę. `taste-skill` każe zdecydować i napisać swoje odczytanie w jednej linii, a pytać tylko o brakujący fakt blokujący pracę. `impeccable` zadaje 2–3 powiązane pytania przed pracą. Cortex pyta, bo brief to najsilniejsza dźwignia na unikalny design.

**2. Idea i trzy kierunki** ([Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md)):
1. Inwentarz tematu: 8–12 rzeczy, które ma tylko ten klient.
2. Argument: każda sekcja to teza z dowodem. Sekcja bez tezy wypada.
3. Koleina: nazwij typową stronę kategorii i jej przeciwieństwo. Obie odpadają.
4. Zdanie idei „Na tej stronie [X z tematu] staje się [środek]” i test konkurenta. Do tego jedna żywa rzecz, którą odwiedzający może zrobić.
5. Pokaż 3 kierunki w różnych rodzinach estetycznych. Każdy ma nazwę, ideę, strategię koloru (Restrained, Committed, Full palette, Drenched), 4–6 kolorów, kroje, layout w jednym zdaniu i ASCII wireframe. Dodaj czwartą, cichą opcję: standard kategorii zrobiony porządnie. Wybiera ją tylko człowiek, nie polecaj jej.

Człowiek wybiera jeden kierunek albo miesza kierunki.

**3. Plan tokenów** dla wybranego kierunku ([Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md)):
- kolor: 4–6 nazwanych wartości w OKLCH, jako tokeny semantyczne z parą `-foreground` ([Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md), [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md)). Jedno tło, jeden tusz, jeden akcent na akcji;
- typografia: 1–2 rodziny i ich role, najwyżej 5 rozmiarów, wyraźny skok od tekstu do nagłówka, tekst ciągły 45–75 znaków ([Podstawy web designu dla developera](web-design-fundamentals.md));
- odstępy: skala 8px, a 4px tylko na ciasne odstępy wewnątrz elementów. Odstęp między sekcjami wyraźnie większy niż wewnątrz sekcji;
- layout: koncepcja w jednym zdaniu, ASCII wireframe, wyrównanie, różna kompozycja sąsiednich sekcji;
- jeden zapamiętywalny element: „spend your boldness in one place”.

**4. Przegląd planu.** Sprawdź, czy któryś wybór wygląda jak domyślny dla każdej podobnej strony. Typowe domyślne wybory:
- krem z terakotą;
- czerń z kwasowym akcentem;
- identyczne karty;
- krój z listy nadużywanych (Inter, Space Grotesk, Fraunces, Playfair…);
- eyebrow nad nagłówkiem;
- wjazd każdej sekcji z animacją.

Jeśli trafisz na któryś, zmień go i napisz, co zmieniłeś ([Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md), [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md)).

**5. Budowa** dokładnie według planu:
1. Najpierw cała treść jako tekst. Nagłówki mają najwyżej 2 linie. Pierwszy ekran mówi, co to jest, i ma prawdziwy przycisk głównej akcji. Każda sekcja z briefu jest kompletna. Dowodów nie wymyślasz: żadnych klientów, opinii ani liczb.
2. Potem kod. Wartości bierzesz tylko z tokenów. Strona ma wyglądać na skończoną bez ruchu.
3. Podłoga jakości: responsywność do mobile, widoczny focus, stany (hover, disabled, loading, error, empty), kontrast WCAG 2.2 AA i ostylowane powierzchnie przeglądarki (zaznaczenie, scrollbar, fokus).
4. Ruch na końcu: jeden zaaranżowany moment, UI poniżej 300 ms, ease-out i `prefers-reduced-motion` ([Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md)).

**6. Przegląd na zrzutach** ([Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md)):
1. Zrób zrzuty 1440, 768 i 390 px.
2. Sprawdź kod według reguł Vercel.
3. Sprawdź UX: werdykt specyficzności, heurystyki Nielsena, problemy P0–P3.
4. Sprawdź obraz: 14 przejść i punktację z limitami.
5. Popraw 3 największe problemy w kolejności: idea → hierarchia → kompozycja → typografia → obrazy → kolor → detale → ruch.

Najwyżej 3 rundy. Na końcu pokaż człowiekowi zrzuty i wynik.

**7. Zapis kierunku.** Zapisz wybrany kierunek i tokeny w `DESIGN.md` projektu ([DESIGN.md — design system w jednym pliku dla agenta](design-md.md)). Kolejne ekrany zostaną wtedy spójne, a kolejne projekty nie powtórzą tego samego kierunku. `impeccable` pisze `DESIGN.md` dla nowego świata dopiero po budowie, z tego, co naprawdę powstało, a nie z planu.

## Jak stosować

Prompt startowy do wklejenia w dowolnym projekcie:

```
Zaprojektuj [co]. Pracuj według design/design-process.md z Cortex.
Zacznij od kroku 1: zadaj mi pytania i poczekaj na odpowiedzi.
```

Skrót dla człowieka:
1. Odpowiedz na pytania.
2. Wybierz jeden z 3 kierunków albo standard.
3. Zatwierdź plan tokenów.
4. Oceń zrzuty i wynik przeglądu.

## Zobacz też
- [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md) — idea z tematu, tryby strony, strategia koloru (krok 2)
- [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) — rubryki przeglądu (krok 6)
- [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md) — zasady ruchu (krok 5)
- [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) — źródło procesu plan → przegląd → budowa → krytyka
- [Prompty do sterowania estetyką designu](design-prompting.md) — dźwignie sterowania estetyką i szablon briefu
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — checklista do kroku 4
- [Katalog popularnych skilli do designu (skills.sh)](design-skills-catalog.md) — skille, które robią podobny proces automatycznie
- [Workflow generowania SVG przez LLM](svg-workflow-llm.md) — osobny proces dla grafik SVG na stronie
