---
title: Przegląd designu — rubryki, punktacja, kolejność poprawek
updated: 2026-10-28
tags: [review, critique, audit, checklist, heuristics, accessibility]
sources:
  - "[vercel-labs/web-interface-guidelines — command.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md) — unknown — high"
  - "[vercel-labs/agent-skills — web-design-guidelines SKILL.md](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines) — unknown — high"
  - "[pbakaus/impeccable — reference/critique.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/critique.md) — unknown — high"
  - "[pbakaus/impeccable — reference/craft-floor.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/craft-floor.md) — unknown — high"
  - "[leonxlnx/taste-skill — references/critique.md](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/references/critique.md) — unknown — medium"
  - "[leonxlnx/taste-skill — SKILL.md](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/SKILL.md) — unknown — medium"
---

# Przegląd designu — rubryki, punktacja, kolejność poprawek

> Popularne skille oceniają design na trzech poziomach. **Kod**: Vercel Web Interface Guidelines, czyli twarde reguły dostępności, formularzy, ruchu i typografii z wynikiem `plik:linia`. **UX**: `impeccable critique`, czyli 10 heurystyk Nielsena na skali 0–4 i priorytety P0–P3. **Obraz**: `taste-skill`, czyli 14 przejść po zrzutach ekranu, punktacja jak u jurora Awwwards i limity punktów za znane tiki. Wspólna zasada: ocenia się wyrenderowany wynik, nie kod ani intencję. Najwyżej trzy rundy poprawek.

## Poziom 1: kod — Vercel Web Interface Guidelines

Skill `web-design-guidelines` przy każdym przeglądzie pobiera świeże reguły z GitHuba i raportuje zwięźle w formacie `plik:linia - problem`. Najważniejsze reguły:

- **Dostępność:** przyciski z samą ikoną mają `aria-label`. `<button>` służy do akcji, `<a>` do nawigacji, nigdy `<div onClick>`. Asynchroniczne komunikaty mają `aria-live="polite"`. Nagłówki tworzą hierarchię, a strona ma link „przejdź do treści”.
- **Fokus:** widoczny `:focus-visible`. Nigdy `outline: none` bez zamiennika. Przyklejony nagłówek nie może zasłaniać elementu z fokusem.
- **Formularze:** pola mają `autocomplete`, poprawny `type` i `inputmode`. Nie blokuj wklejania. Błąd pokazuj przy polu i po wysłaniu ustaw fokus na pierwszym błędzie. Przycisk wysyłania jest aktywny do startu żądania.
- **Ruch:** respektuj `prefers-reduced-motion`. Animuj tylko `transform` i `opacity`. Nigdy `transition: all`. W SVG transformacje dawaj na `<g>` z `transform-box: fill-box; transform-origin: center`.
- **Typografia:** `…` zamiast `...`, cudzysłowy drukarskie, twarde spacje (`10&nbsp;MB`). `tabular-nums` w kolumnach liczb. `text-wrap: balance` na nagłówkach.
- **Treść:** kontenery znoszą długi tekst (`min-w-0` w flex, `line-clamp`). Puste stany są obsłużone.
- **Obrazy:** `<img>` ma `width` i `height` (bez CLS). Poniżej pierwszego ekranu `loading="lazy"`.
- **Stan i nawigacja:** URL odzwierciedla filtry, zakładki i paginację. Akcja niszcząca ma potwierdzenie albo cofnięcie.
- **Motyw ciemny:** `color-scheme: dark` na `<html>`, `<meta name="theme-color">` zgodny z tłem.
- **i18n:** daty i liczby przez `Intl.*`. Nazwy marek z `translate="no"`.
- **Antywzorce do flagowania:** `user-scalable=no`, `transition: all`, `outline-none` bez zamiennika, `<div>` z kliknięciem, obrazy bez wymiarów, pola bez etykiet, `autoFocus` bez powodu.

## Poziom 2: UX — impeccable critique

1. **Werdykt specyficzności (zacznij od tego):** czy wynik wygląda na zrobiony dla tego produktu, czy można go zamienić z dowolnym z kategorii?
2. **Heurystyki Nielsena**, każda 0–4: widoczność stanu, zgodność ze światem, kontrola użytkownika, spójność, zapobieganie błędom, rozpoznawanie zamiast pamiętania, elastyczność, minimalizm, naprawa błędów, pomoc. Na stronach Persuade i Experience heurystyki 7 i 10 mogą być `n/a`. Pasma: 36–40 Excellent, 28–35 Good, 20–27 Acceptable, 12–19 Poor, 0–11 Critical. Według skilla większość prawdziwych interfejsów dostaje 20–32 na 40.
3. **Co działa:** 2–3 rzeczy z uzasadnieniem.
4. **Problemy priorytetowe:** 3–5, każdy z priorytetem.
   - **P0**: blokuje zadanie.
   - **P1**: poważne utrudnienie, napraw przed wydaniem.
   - **P2**: irytuje, ale da się obejść.
   - **P3**: kosmetyka.
   Test: „czy użytkownik napisałby do supportu?” Jeśli tak, to co najmniej P1.
5. **Persony:** wybierz 2–3 pasujące persony, np. zaawansowany użytkownik albo ktoś po raz pierwszy. Dla każdej przejdź główną akcję i wypisz konkretne miejsca, w których coś zawodzi.

**Podłoga jakości** z `craft-floor` (sprawdzana na renderze):
- tekst główny ≥ 4.5:1;
- tekst drugorzędny na kolorowym tle barwiony od tła, nigdy szary;
- cienie mają przesunięcie i rozmycie;
- więcej miejsca nad nagłówkiem niż pod nim;
- tekst ciągły 65–75 znaków;
- stany hover, disabled, loading, error i empty.

Najczęściej pomijane są **powierzchnie przeglądarki**: zaznaczenie tekstu, kursor, paski przewijania, pierścienie fokusu, odstęp podkreślenia i cyfry w tabelach. Ostyluj je z palety.

## Poziom 3: obraz — taste-skill (zrzuty 1440, 768, 390 px)

14 przejść, każde osobno:
1. Jedna sekunda, potem pięć. Co widać i czy obcy wie, co to jest, dla kogo i co zrobić?
2. Zmrużenie oczu. Czy widać 2–3 duże masy?
3. Zakryj logo. Czy strona mogłaby należeć do konkurenta?
4. Krawędzie. Ile jest różnych lewych krawędzi tekstu? Dobrze, gdy 2–3. Sześć znaczy, że elementy stawiano przypadkiem.
5. Odstępy i rama. Czy marginesy są równe i czy są dziury?
6. Typografia. Czy skok od tekstu do nagłówka to co najmniej ×3? Czy jest więcej niż 5 rozmiarów?
7. Kolor. Jakie są proporcje i gdzie jest akcent?
8. Obrazy. Czy są co najmniej 4 prawdziwe zdjęcia i jeden ruchomy obraz?
9. Powtarzalność. Jedno słowo na układ każdej sekcji. To samo słowo dwa razy z rzędu oznacza szablon.
10. Telefon. Czy to osobna kompozycja, a nie ściśnięty desktop?
11. Pełność. Czy każdy ekran to plakat, a nie wąska kolumna?
12. Treść. Czy każda sekcja z briefu jest kompletna i czy na pierwszym ekranie jest przycisk akcji?
13. Kolizje. Czy coś zasłania nagłówek albo wystaje poza ekran telefonu?
14. Test konkurenta i jedna żywa rzecz.

**Punktacja** 1–10 w czterech kryteriach: design 40%, użyteczność 30%, kreatywność 20%, treść 10%. Według skilla prawdziwe strony wyróżnione jako Site of the Day mają u jurorów około 7.5–8.0. Jeśli dajesz sobie 9, oceń jeszcze raz.

**Limity** nadpisują arytmetykę, np.:
- eyebrow, numeracja 01/02/03, gradient dekoracyjny albo nagłówek w 3 liniach → całość maksymalnie 6.5;
- strona mogłaby należeć do każdego → kreatywność maksymalnie 6;
- brak przycisku akcji na pierwszym ekranie → użyteczność maksymalnie 7;
- placeholder → treść maksymalnie 5.

> Ostrzeżenie z testów `taste-skill`: w ślepych porównaniach bogatsza strona z tikami szablonu zawsze wygrywała z czystszą, ale pustą. Usunięcie ozdobników to połowa pracy. Druga połowa to treść, skala i prawdziwe obrazy.

## Kolejność poprawek (taste-skill)

Później poprawiane rzeczy nie uratują wcześniejszych:
1. idea;
2. hierarchia, czyli jeden dominujący element na ekran;
3. kompozycja;
4. typografia;
5. obrazy;
6. kolor;
7. detale i stany;
8. ruch na końcu.

Najwyżej 3 rundy: krytyka, poprawa 3 największych problemów, nowe zrzuty. Jeśli po 3 rundach wynik jest poniżej 7.5, powiedz to wprost.

## Jak stosować

Prompt przeglądu do wklejenia:

```
Przejrzyj [stronę/pliki] w trzech krokach i zapisz wynik:
1. Kod: reguły Vercel Web Interface Guidelines, wynik jako plik:linia - problem.
2. UX: werdykt specyficzności (czy to strona tego produktu, czy dowolnej z kategorii),
   10 heurystyk Nielsena 0–4 z sumą, 3–5 problemów z priorytetem P0–P3.
3. Obraz: zrzuty 1440/768/390. Dla każdego: co widać w 1 sekundę, test zakrytego logo,
   liczba lewych krawędzi, słowo-układ każdej sekcji. Punkty: design·0.4 + użyteczność·0.3
   + kreatywność·0.2 + treść·0.1, z limitami za eyebrow, 01/02/03, gradient, brak CTA.
Potem popraw 3 największe problemy w kolejności: idea → hierarchia → kompozycja →
typografia → obrazy → kolor → detale → ruch. Maksymalnie 3 rundy.
```

## Zobacz też
- [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md) — przegląd to krok 6 procesu
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — lista tików, które obniżają limity
- [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md) — osobny przegląd animacji
- [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md) — progi kontrastu
- [Katalog popularnych skilli do designu (skills.sh)](design-skills-catalog.md) — skille, z których pochodzą te rubryki
