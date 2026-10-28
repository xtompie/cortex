---
title: Ruch w interfejsie — kiedy animować, easing, czasy, przegląd
updated: 2026-10-28
tags: [motion, animation, easing, interaction, review, accessibility]
sources:
  - "[emilkowalski/skills — emil-design-eng SKILL.md](https://github.com/emilkowalski/skills/blob/main/skills/emil-design-eng/SKILL.md) — unknown — high"
  - "[emilkowalski/skills — review-animations SKILL.md](https://github.com/emilkowalski/skills/blob/main/skills/review-animations/SKILL.md) — unknown — high"
  - "[pbakaus/impeccable — reference/craft-floor.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/craft-floor.md) — unknown — high"
  - "[leonxlnx/taste-skill — SKILL.md](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/SKILL.md) — unknown — medium"
  - "[vercel-labs/web-interface-guidelines — command.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md) — unknown — high"
---

# Ruch w interfejsie — kiedy animować, easing, czasy, przegląd

> Emil Kowalski (autor Sonnera) ustala kolejność decyzji. Najpierw: czy to w ogóle animować, zależnie od tego, jak często użytkownik to widzi. Potem: po co. Potem: jaki easing. Na końcu: jak szybko. Akcje z klawiatury i rzeczy widziane setki razy dziennie nie mają animacji. Animacje UI trwają poniżej 300 ms, z mocnym ease-out i tylko na `transform` i `opacity`. Na stronach marketingowych skille spierają się, ile ruchu jest potrzebne.

## Cztery decyzje (emil-design-eng)

**1. Czy animować?** Zależy od częstotliwości:

| Jak często | Decyzja |
|---|---|
| 100+ razy dziennie (skróty klawiszowe, paleta komend) | bez animacji |
| dziesiątki razy dziennie (hover, nawigacja po liście) | usuń albo mocno ogranicz |
| okazjonalnie (modale, szuflady, toasty) | standardowa animacja |
| rzadko, pierwszy raz (onboarding, świętowanie) | można dodać zachwyt |

Nigdy nie animuj akcji wywołanych klawiaturą. Raycast nie ma animacji otwarcia i zamknięcia.

**2. Po co?** Poprawne cele: spójność przestrzenna (toast wjeżdża i wyjeżdża z tej samej strony), pokazanie zmiany stanu, wyjaśnienie, informacja zwrotna (przycisk lekko się zmniejsza przy naciśnięciu) i uniknięcie skoku. „Wygląda fajnie” przy częstym elemencie nie jest celem.

**3. Easing:**
- wejście i wyjście → ease-out;
- ruch po ekranie → ease-in-out;
- hover i kolor → ease;
- ruch stały (marquee, pasek postępu) → linear;
- nigdy ease-in w UI, bo opóźnia moment, na który użytkownik patrzy.

Wbudowane krzywe CSS są za słabe. Użyj własnych:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1); /* iOS-like, z Ionic */
```

**4. Czas:**
- informacja po naciśnięciu przycisku: 100–160 ms;
- tooltipy: 125–200 ms;
- dropdowny: 150–250 ms;
- modale i szuflady: 200–500 ms.

Animacje UI trwają poniżej 300 ms. Szybciej znaczy też „aplikacja wydaje się szybsza”: dropdown 180 ms odbierasz jako bardziej responsywny niż 400 ms.

## Zasady komponentów

- Przycisk: `:active { transform: scale(0.97) }`. Skala 0.95–0.98.
- Nigdy nie animuj od `scale(0)`. Startuj od `scale(0.95)` z `opacity: 0`.
- Popover rośnie od swojego przycisku (`transform-origin` z wyzwalacza). Modal jest wyjątkiem: zostaje na środku.
- Tooltipy: pierwszy z opóźnieniem, kolejne natychmiast i bez animacji.
- Do elementów wywoływanych szybko (toasty, przełączniki) używaj przejść CSS albo sprężyn, nie keyframes. Przejście można przerwać i przekierować. Keyframes startują od zera.
- Crossfade wygląda źle? Dodaj `filter: blur(2px)` w trakcie przejścia, ale poniżej 20px, bo blur jest drogi w Safari.
- Wejście bez JS: `@starting-style`.
- Sprężyny do przeciągania, gestów i elementów „żywych”. Odbicie subtelne, 0.1–0.3. Przykład konfiguracji: `{ type: "spring", duration: 0.5, bounce: 0.2 }`.
- Asymetria: świadome akcje (przytrzymanie, potwierdzenie usunięcia) animują się wolniej, a odpowiedzi systemu natychmiast.

## Dostępność i wydajność

- `prefers-reduced-motion` znaczy mniej i łagodniej, nie zero. Zostaw przejścia opacity i koloru, usuń ruch.
- Animacje na hover zamykaj w `@media (hover: hover) and (pointer: fine)`, bo dotyk wywołuje hover przy tapnięciu.
- Animuj tylko `transform` i `opacity`. Nigdy `width`, `height`, `margin`, `top` ani `transition: all`.
- Animacje CSS działają lepiej od JS pod obciążeniem. Do animacji programowych używaj WAAPI.
- Vercel: animacje muszą dać się przerwać. Ruch dłuższy niż 5 sekund obok treści potrzebuje pauzy.

## Ruch na stronach marketingowych

> **Status: Disputed** — Skille różnią się, ile ruchu potrzebuje strona.
> - `taste-skill` wymaga warstwy ruchu: sekwencja wejść dla części każdej sekcji (nagłówek, tekst, obraz z opóźnieniem 60–90 ms, uniesienie 16–32 px), co najmniej 8 poruszających się elementów i jeden ruchomy obraz.
> - `impeccable` craft-floor: „one authored moment, not scattered effects and not one identical entrance on every section”.
> - Anthropic `frontend-design` (2026-09) uznaje wjazd każdej sekcji za znak AI.
> - Wspólne: jeden zaaranżowany moment jest najważniejszy, treść jest widoczna bez skryptu, a jednakowy fade na każdym bloku jest zły. `taste-skill` też obniża ocenę za „one identical fade on every block”.

## Przegląd animacji (review-animations)

Dziesięć standardów:
1. ruch ma uzasadnienie;
2. ilość ruchu pasuje do częstotliwości;
3. easing jest responsywny;
4. animacje UI trwają poniżej 300 ms;
5. `transform-origin` jest poprawny, bez `scale(0)`;
6. animację można przerwać;
7. animowane są tylko właściwości obsługiwane przez GPU;
8. ruch jest dostępny;
9. wejście i wyjście mają asymetryczne czasy;
10. ruch pasuje do charakteru produktu.

Kolejność poprawek, od najlepszej:
1. usuń animację;
2. zmniejsz ją;
3. popraw easing;
4. popraw origin;
5. zrób ją przerywalną;
6. przenieś na GPU;
7. ustaw asymetryczne czasy;
8. dopracuj (blur, stagger, `@starting-style`);
9. dostępność i spójność.

## Jak stosować

Pytania przed każdą animacją:

```
1. Jak często użytkownik to zobaczy? (100+/dzień → brak animacji)
2. Po co to się rusza? (stan / przestrzeń / feedback / wyjaśnienie / uniknięcie skoku)
3. Wejście/wyjście → ease-out cubic-bezier(0.23, 1, 0.32, 1). Nigdy ease-in.
4. Czas < 300 ms dla UI. Tylko transform + opacity.
5. prefers-reduced-motion: zostaw opacity, usuń ruch. Hover za (hover: hover) and (pointer: fine).
```

Przegląd w formie tabeli: `| Przed | Po | Dlaczego |`, jeden wiersz na problem.

## Zobacz też
- [Techniki SVG na web — viewBox, prymitywy, dostępność, animacja](svg-techniques.md) — animacja SVG (CSS, WAAPI, SMIL)
- [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) — ruch jako ostatni punkt kolejności poprawek
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — ruch jako znak designu z AI
